---
title: parseGTF.py
layout: post
categories:
  - scripts
  - python
  - scripts
tags:
  - python
---

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#from __future__ import division, with_statement
'''
Copyright 2010, chentong (chentong_biology@163.com).  
Please see the license file for legal information.
===========================================================
'''
__author__ = 'chentong & ct586[9]'
__author_email__ = 'chentong_biology@163.com'
#=========================================================
import sys
if False:
    print >>sys.stderr, "This program does not work under python 3, \
run in python 2.x."

from time import localtime, strftime 
timeformat = "%Y-%m-%d %H:%M:%S"

'''
File format (The transcript IDs are assumed to be uniq especially for
neighboring genes. Lines containing CDS in the third column is not
necessary. Those lines will just be ignored. Only lines with 'exon',
'start_codon', 'stop_codon' are used.)

chr1    refGene exon    3204563 3207049 .   -   .   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "1"; exon_id "NM_001011874.1"; gene_name "Xkr4";
chr1    refGene stop_codon  3206103 3206105 .   -   0   gene_id "Xkr4"; transcript_id "NM_001011874"; exon_number "1"; exon_id "NM_001011874.1"; gene_name "Xkr4";
chr1    refGene CDS 3206106 3207049 .   -   2   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "1"; exon_id "NM_001011874.1"; gene_name "Xkr4";
chr1    refGene CDS 3411783 3411982 .   -   1   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "2"; exon_id "NM_001011874.2"; gene_name "Xkr4";
chr1    refGene exon    3411783 3411982 .   -   .   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "2"; exon_id "NM_001011874.2"; gene_name "Xkr4";
chr1    refGene CDS 3660633 3661429 .   -   0   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "3"; exon_id "NM_001011874.3"; gene_name "Xkr4";
chr1    refGene exon    3660633 3661579 .   -   .   gene_id "Xkr4";transcript_id "NM_001011874"; exon_number "3"; exon_id "NM_001011874.3"; gene_name "Xkr4";
chr1    refGene start_codon 3661427 3661429 .   -   0   gene_id "Xkr4"; transcript_id "NM_001011874"; exon_number "1"; exon_id "NM_001011874.1"; gene_name "Xkr4";


Tested for the following status (start_condon and stop_codon can span
two exons):
exon-ATT-exon-intron-exon-intron-exon-UAA-exon
exon-ATT-exon-UAA-exon
exon-AT-intron-T-exon-interon-exon-UA-intron-A-exon
'''



def flankTSS_TES(TSS, TTS, end, regionL, strand, name_base, score, chr):
    #-------end means chromosome end-----------
    for seg in regionL:
        #--------------TSS---------------------------
        newstart = TSS - seg/2
        if newstart < 0: newstart = 0
        newend   = TSS + seg/2
        if newend > end: newend = end
        if strand == '+':
            name = name_base + '.TSS' + str(seg)
        elif strand == '-':
            name = name_base + '.TTS' + str(seg)
        tmpLineL = [chr,str(newstart),str(newend),name, \
            score,strand]
        print "\t".join(tmpLineL)
        #------------TES---------------------------
        newstart = TTS - seg/2
        if newstart < 0: newstart = 0
        newend   = TTS + seg/2
        if newend > end: newend = end
        if strand == '+':
            name = name_base + '.TTS' + str(seg)
        elif strand == '-':
            name = name_base + '.TSS' + str(seg)
        tmpLineL = [chr,str(newstart),str(newend),name, \
            score,strand]
        print "\t".join(tmpLineL)
    #--------------------------------------
#------------------------------------------------------


def outTSS_TES(TSS, TTS, end, regionL, strand, name_base, score, chr):
    oldseg = 0
    for seg in regionL:
        #--------------TSS---------------------------
        newstart = TSS - seg
        if newstart < 0: newstart = 0
        newend = TSS - oldseg
        if newend > 0:
            if strand == '+':
                name = name_base + '.TSS-UP' + str(oldseg) + '-' + str(seg)
            elif strand == '-':
                name = name_base + '.TTS-DW' + str(oldseg) + '-' + str(seg)
            tmpLineL = [chr,str(newstart),str(newend),name, \
                score,strand]
            print "\t".join(tmpLineL)
        #------------TES---------------------------
        newstart = TTS + oldseg
        newend   = TTS + seg
        if newend > end: newend = end
        if newstart < end:
            if strand == '+':
                name = name_base + '.TTS-DW' + str(oldseg) + '-' + str(seg) 
            elif strand == '-':
                name = name_base + '.TSS-UP' + str(oldseg) + '-' + str(seg) 
            tmpLineL = [chr,str(newstart),str(newend),name, \
                score,strand]
            print "\t".join(tmpLineL)
        #--------update oldseg-------------------------
        oldseg = seg
    #--------------------------------------
#------------------------------------------------------

def get_gene_body(chr,keyL,tmpDict,name,score,strand):
    allpos_start = [ele[0] for ele in keyL]
    allpos_stop = [ele[1] for ele in keyL]
    allpos_start.sort()
    allpos_stop.sort()
    tmpLineL = [chr,str(allpos_start[0]),str(allpos_stop[-1]),name, score,strand]
    print '\t'.join(tmpLineL)
    return allpos_start[0], allpos_stop[-1]-1
#-------------------------------------------------------


def get_coding_exon_intron(chr,keyL,tmpDict,name,score,strand):
    oldEle = ''
    intron_num = 1
    exon_num = 1
    intron_start = -1
    begin_coding_exon = 0
    end_coding_exon   = 0
    oneMoreExonNeeded = 0
    ExonL = []
    tmpLineL_218 = ''
    first_met_stop_codon = 1
    first_met_start_codon = 1
    #print keyL
    for ele in keyL:
        if strand == '+':
            if tmpDict[ele] == 'exon':
                #--------intron----------------------
                if intron_start == -1:
                    intron_start = ele[1]
                else:
                    intron = name + '.Intron.'+str(intron_num)
                    intron_num += 1
                    tmpLineL = [chr,str(intron_start),str(ele[0]),intron,score,
                        strand]
                    intron_start = ele[1]
                    print '\t'.join(tmpLineL)
                #--------intron----------------------
                #---------output exon after start_codon meets---
                if begin_coding_exon and not end_coding_exon:
                    exon = name + '.Coding_exon.'+str(exon_num)
                    exon_num += 1
                    tmpLineL = [chr,str(ele[0]),str(ele[1]),exon,score,
                        strand]
                    ExonL.append(tmpLineL[:])
                    if tmpLineL_218:
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    #print '\t'.join(tmpLineL)
                if oneMoreExonNeeded:
                    if exonEnd > ele[0]:
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL = [chr,str(ele[0]),str(exonEnd),exon,score,
                            strand]
                        print '\t'.join(tmpLineL)
                    oneMoreExonNeeded = 0
                #---------output exon after start_codon meets---
                oldEle = ele
                #-----------------------------------
            #------------------------------------------
            elif tmpDict[ele] == 'start_codon':
                if not begin_coding_exon:
                    #In case start_codon is the first one
                    if oldEle and oldEle[1] > ele[0] >= oldEle[0]:
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL_218 = [chr,str(ele[0]),str(oldEle[1]),exon,score,
                            strand]
                        #print '\t'.join(tmpLineL)
                    begin_coding_exon = 1
            elif tmpDict[ele] == 'stop_codon':
                #here = 0
                if not first_met_stop_codon:
                    exon = name + '.Coding_exon.'+str(exon_num)
                    exon_num += 1
                    tmpLineL = [chr,str(ele[0]),str(ele[1]),exon,score,
                        strand]
                    print '\t'.join(tmpLineL)
                elif first_met_stop_codon:
                    first_met_stop_codon = 0
                    for i in ExonL[:-1]:
                        #here = 1
                        print '\t'.join(i)
                    #if here:
                    #exon_num -= 1
                    #---------------If only one exon----------------
                    if tmpLineL_218 and ele[1] <= int(tmpLineL_218[2]):
                        tmpLineL_218[2] = str(ele[1])
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    #---------------If only one exon----------------
                    elif tmpLineL_218 and ele[1] > int(tmpLineL_218[2]):
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    elif oldEle[0] < ele[1] <= oldEle[1]:
                        exon_num -= 1
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL = [chr,str(oldEle[0]),str(ele[1]),exon,score,
                            strand]
                        print '\t'.join(tmpLineL)
                    if ele[1] > oldEle[1]:
                        #print oldEle, ExonL
                        if ExonL:
                            assert int(ExonL[-1][2]) == oldEle[1]
                            print '\t'.join(ExonL[-1])
                        oneMoreExonNeeded = 1
                        exonEnd = ele[1]
                    #---this can never happen----
                    #if ele[1] > oldEle[1]:
                    #    oneMoreExonNeeded = 1
                    #    exonEnd = ele[1]
                    end_coding_exon = 1
            #--------END +----------------------------------------
        #-------------END + strand----------------------
        elif strand == '-':
            if tmpDict[ele] == 'exon':
                #---------output intron-------------------------
                if intron_start == -1:
                    intron_start = ele[1]
                else:
                    intron = name + '.Intron.'+str(intron_num)
                    intron_num += 1
                    tmpLineL = [chr,str(intron_start),str(ele[0]),intron,score,
                        strand]
                    intron_start = ele[1]
                    print '\t'.join(tmpLineL)
                #---------output intron-------------------------
                #---------output exon after start_codon meets---
                if begin_coding_exon and not end_coding_exon:
                    exon = name + '.Coding_exon.'+str(exon_num)
                    exon_num += 1
                    tmpLineL = [chr,str(ele[0]),str(ele[1]),exon,score,
                        strand]
                    ExonL.append(tmpLineL[:])
                    #---output exon defined by stop_codon
                    if tmpLineL_218:
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    new_exon = 1
                    #print '\t'.join(tmpLineL)
                if oneMoreExonNeeded:
                    if exonEnd > ele[0]:
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL = [chr,str(ele[0]),str(exonEnd),exon,score,
                            strand]
                        print '\t'.join(tmpLineL)
                    oneMoreExonNeeded = 0
                #---------output exon after start_codon meets---
                oldEle = ele
            #----------------------END if--------------------
            elif tmpDict[ele] == 'stop_codon':
                if not begin_coding_exon:
                    #In case stop_codon is the first one
                    if oldEle and oldEle[1] > ele[0] >= oldEle[0]:
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL_218 = [chr,str(ele[0]),str(oldEle[1]),exon,score,
                            strand]
                        #print >>sys.stderr, '\t'.join(tmpLineL)
                    begin_coding_exon = 1
                    new_exon = 0
            elif tmpDict[ele] == 'start_codon':
                #here = 0
                if not first_met_start_codon:
                    #if tmpLineL_218 and ele[1] > int(tmpLineL_218[2]):
                        #----two exons,  but start_codon is the begin
                        #of last exon
                    #    print '\t'.join(tmpLineL_218)
                    #    tmpLineL_218 = ''
                    exon = name + '.Coding_exon.'+str(exon_num)
                    exon_num += 1
                    tmpLineL = [chr,str(ele[0]),str(ele[1]),exon,score,
                        strand]
                    print '\t'.join(tmpLineL)
                    #oneMoreExonNeeded = 0
                elif first_met_start_codon:
                    #print ele[1],oldEle[1],tmpLineL_218
                    first_met_start_codon = 0
                    for i in ExonL[:-1]:
                        #here = 1
                        print '\t'.join(i)
                    #if here:
                    #exon_num -= 1
                    #---------------If only one exon----------------
                    if tmpLineL_218 and ele[1] <= int(tmpLineL_218[2]):
                        tmpLineL_218[2] = str(ele[1])
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    #---------------If only one exon----------------
                    #This will hit----------------------
                    elif tmpLineL_218 and ele[1] > int(tmpLineL_218[2]):
                        #----two exons,  but start_codon is the begin
                        #of last exon
                        print '\t'.join(tmpLineL_218)
                        tmpLineL_218 = ''
                    elif oldEle[0] < ele[1] <= oldEle[1]:
                        exon_num -= 1
                        exon = name + '.Coding_exon.'+str(exon_num)
                        exon_num += 1
                        tmpLineL = [chr,str(oldEle[0]),str(ele[1]),exon,score,
                            strand]
                        print '\t'.join(tmpLineL)
                    #This will hit----------------------
                    if ele[1] > oldEle[1]:
                        #--Output only when new exons met--
                        #print oldEle, ExonL
                        if ExonL:
                            assert int(ExonL[-1][2]) == oldEle[1]
                            print '\t'.join(ExonL[-1])
                        #--Output only when new exons met--
                        oneMoreExonNeeded = 1
                        exonEnd = ele[1]
                    end_coding_exon = 1
        #--------END -----------------------------------------
    #------------END for ele------------------------------
    #----for NR--------------
    if first_met_stop_codon and first_met_start_codon:
        for ele in keyL:
            exon = name + '.Coding_exon.'+str(exon_num)
            exon_num += 1
            tmpLineL = [chr,str(ele[0]),str(ele[1]),exon,score,
                strand]
            print '\t'.join(tmpLineL)
    #----for NR--------------
#-------------------end get_coding_exon_intron_genebody--------
'''
tmpDict = {strand:'+',  (0, 100):'exon', (80, 83):'start_codon', \
        (1000, 1003):'stop_codon', (700, 1500):'exon'}
'''

def parse(tmpDict, key, name_label,cs_dict,regionL):
    strand = tmpDict.pop('strand')
    chr    = tmpDict.pop('chr')
    chrom_end = cs_dict[chr]
    score, name, unused_315 = key.split('#')
    name += '_'+name_label
    keyL = tmpDict.keys()
    #keyL.sort(key=lambda x:x[0])
    keyL.sort()
    get_coding_exon_intron(chr,keyL,tmpDict,name,'0',strand)
    start, end = get_gene_body(chr,keyL,tmpDict,name,score,strand)
    flankTSS_TES(start, end, chrom_end, regionL, strand, name, '0', chr)
    outTSS_TES(start, end, chrom_end, regionL, strand, name, '0', chr)
    if strand == '+':
        #------find UTR5--------------
        tmpL = []
        needOneMoreExon = 0
        all_UTR3 = 0
        #---stop_codons span two exons---
        stop_codon_unfinished = 0
        start_codon_unfinished = 0
        stop_codon_cnt = 0
        for key in keyL:
            if tmpDict[key] == "exon":
                tmpL.append(key)
                if all_UTR3 and not needOneMoreExon:
                    tmpLineL = [chr,str(key[0]),str(key[1]),UTR3,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                    continue
            elif tmpDict[key] == "start_codon":
                #if start_codon is the first one, no UTR5
                if not tmpL:
                    continue
                #if start codon spans multile exons, ignore its end
                #position
                if start_codon_unfinished:
                    continue
                UTR5 = name + '.UTR5'
                #------for UTRs span multiple exons----
                #intron_start = -1
                if len(tmpL) > 1:
                    for ele in tmpL[:-1]:
                        tmpLineL = [chr,str(ele[0]),str(ele[1]),UTR5,'0',
                            strand]
                        print '\t'.join(tmpLineL)
                        #------------intron-------------------------
                        #if intron_start == -1:
                        #    intron_start = ele[1]
                        #else:
                        #    intron = name + '.Intron.'+str(intron_num)
                        #    intron_num += 1
                        #    tmpLineL = [chr,str(intron_start),str(ele[0]),intron,'0',
                        #       strand]
                        #    intron_start = ele[1]
                        #    print '\t'.join(tmpLineL)
                        #-----------intron-------------------------
                #-----for UTRs overlapped with exon---------------------- 
                #--Only need the start site of start_condon-----
                #----------------intron----------------------------
                #if intron_start == -1:
                #    intron_start = tmpL[-1][1]
                #else:
                #    intron = name + '.Intron.'+str(intron_num)
                #    intron_num += 1
                #    tmpLineL = [chr,intron_start,tmpL[-1][0],intron,'0',
                #        strand]
                #    intron_start = tmpL[-1][1]
                #    print '\t'.join(tmpLineL)
                #----------------intron----------------------------
                #This assert can not be right if the start_codon begins
                #at the next exon.
                #assert tmpL[-1][0] <= key[0] <= tmpL[-1][1]
                #assert tmpL[-1][0] <= key[0] <= tmpL[-1][1]
                if tmpL[-1][1] >= key[0] > tmpL[-1][0]:
                    tmpLineL = [chr,str(tmpL[-1][0]),str(key[0]),UTR5,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                    #-------------coding exon---------------------------
                    #if key[0] < tmpL[-1][1]:
                    #    cod_exon = name + '.Coding_exon.' + str(exon_num)
                    #    exon_num += 1
                    #    tmpLineL = [chr,key[0],tmpL[-1][1],cod_exon,score,
                    #        strand]
                    #    print '\t'.join(tmpLineL)
                    #-------------coding exon---------------------------
                elif key[0] > tmpL[-1][1]:
                    tmpLineL = [chr,str(tmpL[-1][0]),str(tmpL[-1][1]),UTR5,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                if key[1] - key[0] < 3:
                    start_codon_unfinished = 1
            #-------------------end UTR5------------------------
            elif tmpDict[key] == "stop_codon":
                #--this is used to record the end of stop_codon
                if stop_codon_unfinished:
                    end_stop_codon = key[1]
                    stop_codon_cnt += key[1]-key[0]
                    #this continue is usd to read in another exon
                #--this is used to record the end of stop_codon
                else:
                    all_UTR3 = 1
                    UTR3 = name + '.UTR3'
                    lastExon = tmpL[-1]
                    #This assert could not be allowed when stop codon
                    #begins at one exon.
                    #assert lastExon[0] <= key[0] <= lastExon[1], name
                    ##if key[1] == lastExon[1],  UTR must start at the
                    #next exon 
                    if key[1] < lastExon[1]:
                        tmpLineL = [chr,str(key[1]),str(lastExon[1]),UTR3,'0',
                            strand]
                        print '\t'.join(tmpLineL)
                    elif key[1] == lastExon[1] and key[1]-key[0]<3:
                        stop_codon_unfinished = 1
                        stop_codon_cnt += key[1]-key[0]
                        needOneMoreExon = 1
                        end_stop_codon  = key[1]
                        tmpL = []
                    elif key[1] > lastExon[1] and key[0] < lastExon[1]:
                        print >>sys.stderr, "This should never happen"
                        sys.exit(1)
                        needOneMoreExon = 1
                        end_stop_codon  = key[1]
                        tmpL = []
                        stop_codon_cnt = 3
                    if key[0] >= lastExon[1]:
                        needOneMoreExon = 1
                        stop_codon_cnt = key[1]-key[0]
                        end_stop_codon = key[1]
                        tmpL = []
                    #------------------------------
                #---------------------------------
            #---------------------------------------
            if needOneMoreExon and tmpL and stop_codon_cnt == 3:
                assert (len(tmpL) == 1) 
                if end_stop_codon >= tmpL[0][0]:
                    tmpLineL = [chr,str(end_stop_codon),str(tmpL[0][1]),UTR3,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                else:
                    tmpLineL = [chr,str(tmpL[0][0]),str(tmpL[0][1]),UTR3,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                #--------------------------------------
                needOneMoreExon = 0           
            #--------End <needOneMoreExon>-------------
        #-------------end iterating---------------
        #-------------find UTR5 and UTR3----------------
    elif strand == '-':
        #TSS = keyL[-1][1] - 1
        #TTS = keyL[0][0]
        #flankTSS_TES(TSS, TTS, chrom_end, regionL, strand, name, '0', chr)
        #outTSS_TES(TSS, TTS, chrom_end, regionL, strand, name, '0', chr)
        #------find UTR5--------------
        tmpL = []
        needOneMoreExon = 0
        all_UTR5 = 0
        start_codon_unfinished = 0
        stop_codon_unfinished = 0
        start_codon_cnt = 0
        #print keyL
        for key in keyL:
            if tmpDict[key] == "exon":
                tmpL.append(key)
                if all_UTR5 and not needOneMoreExon:
                    tmpLineL = [chr,str(key[0]),str(key[1]),UTR5,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                    continue
            elif tmpDict[key] == "stop_codon":
                #if stop_codon is the first one, no UTR3
                if not tmpL:
                    continue
                if stop_codon_unfinished:
                    continue
                UTR3 = name + '.UTR3'
                #------for UTRs span multiple exons
                if len(tmpL) > 1:
                    for ele in tmpL[:-1]:
                        tmpLineL = [chr,str(ele[0]),str(ele[1]),UTR3,'0',
                            strand]
                        print '\t'.join(tmpLineL)
                #-----for UTRs overlapped with exon---------------------- 
                #--Only need the start site of start_condon-----
                #This assert can not be right if the stop_codon begins
                #at the next exon.
                #assert tmpL[-1][0] <= key[0] <= tmpL[-1][1]
                if tmpL[-1][1] >= key[0] > tmpL[-1][0]:
                    tmpLineL = [chr,str(tmpL[-1][0]),str(key[0]),UTR3,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                elif key[0] > tmpL[-1][1]:
                    tmpLineL = [chr,str(tmpL[-1][0]),str(tmpL[-1][1]),UTR3,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                if key[1] - key[0] < 3:
                    stop_codon_unfinished = 1
            #-------------------end UTR3------------------------
            elif tmpDict[key] == "start_codon":
                #--this is used to record the end of stop_codon
                if start_codon_unfinished:
                    begin_start_codon = key[1]
                    start_codon_cnt += key[1]-key[0]
                    #this continue is usd to read in another exon
                    #continue
                #--this is used to record the end of stop_codon
                else:
                    all_UTR5 = 1
                    UTR5 = name + '.UTR5'
                    #print tmpL
                    lastExon = tmpL[-1]
                    #This assert could not be allowed when start codon
                    #begins at one exon.
                    #assert lastExon[0] <= key[0] <= lastExon[1], name
                    #This assert is used to make sure if codon spans
                    #multiple exons,  it will be separated into several
                    #segments.
                    #assert key[1] <= lastExon[1]
                    if key[1] < lastExon[1]:
                        tmpLineL = [chr,str(key[1]),str(lastExon[1]),UTR5,'0',
                            strand]
                        print '\t'.join(tmpLineL)
                    elif key[1] == lastExon[1] and key[1]-key[0]<3:
                        start_codon_unfinished = 1
                        start_codon_cnt += key[1]-key[0]
                        needOneMoreExon = 1
                        begin_start_codon  = key[1]
                        tmpL = []
                    elif key[1] > lastExon[1] and key[0] < lastExon[1]:
                        print >>sys.stderr, key[1],lastExon[1],name
                        print >>sys.stderr, "This should never happen"
                        sys.exit(1)
                        needOneMoreExon = 1
                        begin_start_codon = key[1]
                        tmpL = []
                        start_codon_cnt = key[1]-key[0]
                    if key[0] >= lastExon[1]:
                        needOneMoreExon = 1
                        start_codon_cnt = key[1]-key[0]
                        begin_start_codon = key[1]
                        tmpL = []
                    #---------------------------------
                #------------------------------------
            #----to deal with stop_codon at the end of exon--------------------
            if needOneMoreExon and tmpL and start_codon_cnt == 3:
                if begin_start_codon >= tmpL[0][0]:
                    tmpLineL = [chr,str(begin_start_codon),str(tmpL[0][1]),UTR5,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                else:
                    tmpLineL = [chr,str(tmpL[0][0]),str(tmpL[0][1]),UTR5,'0',
                        strand]
                    print '\t'.join(tmpLineL)
                #--------------------------------------
                needOneMoreExon = 0           
            #--------End <needOneMoreExon>-------------
        #-------------end iterating---------------
        #-------------find UTR5 and UTR3----------------
#---------------------------------------

def main():
    lensysargv = len(sys.argv)
    if lensysargv < 3:
        print >>sys.stderr, "This parses GTF file to extract UTR5, \
UTR3, coding exon, intron, TSS, TTS, upstream and downstream regions."
        print >>sys.stderr, 'Using python %s filename[GTF, sorted \
first by gene, then column 4 and 5(using program sortGTF.py); - means \
sys.stdin] chromsome_size' % sys.argv[0]
        sys.exit(0)
    #-----------------------------------
    regionL = [500,1000,2000,5000]
    accepted_regionL = ['exon', 'stop_codon', 'start_codon']
    #------get chromosome size-----------------
    chrom_size = sys.argv[2]
    cs_dict = {}
    for line in open(chrom_size):
        lineL = line.split()
        cs_dict[lineL[0]] = int(lineL[1])
    #------get chromosome size-----------------
    file = sys.argv[1]
    if file == '-':
        fh = sys.stdin
    else:
        fh = open(file)
    #-------------------------------------------
    name_label = 0
    tmpDict = {}
    oldname = ""
    for line in fh:
        lineL = line.split("\t")
        region_name = lineL[2]
        # GTF coordinate starts with 1. Here transfer to bed format.
        if region_name in accepted_regionL:
            start_end = (int(lineL[3])-1,int(lineL[4])) 
            attributeL = lineL[8].split('; ')[:2]
            gene_id = attributeL[0].replace("gene_id ", "").strip('\"')
            transcript_id = attributeL[1].replace("transcript_id ","").strip('\"')
            key = '#'.join([gene_id, transcript_id, lineL[0]])
            if oldname != "" and oldname != key:
                name_label += 1
                parse(tmpDict[oldname],oldname,str(name_label),cs_dict,regionL)
                tmpDict = {}
            #-------------------------------------------------------
            oldname = key
            if key not in tmpDict:
                tmpDict[key] = {}
                tmpDict[key]['strand'] = lineL[6]
                tmpDict[key]['chr'] = lineL[0]
            if start_end not in tmpDict[key]:
                tmpDict[key][start_end] = region_name
            else:
                print >>sys.stderr, "Duplicate start_end (%d, %d) \
                    for %s" % (start_end[0], start_end[1], key)
                sys.exit(1)
            #--------------------------------------------------
        #--------------end filtering lines-----------------------
    #------------------end reading----------------------------
    #---deal with the last element in tmpDict-----------
    if tmpDict:
        name_label += 1
        parse(tmpDict[oldname],oldname,str(name_label),cs_dict,regionL)
        tmpDict = {}
    #----close file handle for files-----
    if file != '-':
        fh.close()
    #-----------end close fh-----------
#------------------------------------------------------
    #-------------END reading file----------
if __name__ == '__main__':
    startTime = strftime(timeformat, localtime())
    main()
    endTime = strftime(timeformat, localtime())
    fh = open('python.log', 'a')
    print >>fh, "%s\n\tRun time : %s - %s " % \
        (' '.join(sys.argv), startTime, endTime)
    fh.close()



{% endhighlight %}

##### All types of special GTF structures processed during writing scripts.
>chr2	refGene	stop_codon	176083705	176083707	.	-	0	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "1"; exon_id "NM_001099327.1"; gene_name "100043387";
chr2	refGene	exon	176083705	176085010	.	-	.	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "1"; exon_id "NM_001099327.1"; gene_name "100043387";
chr2	refGene	exon	176086169	176086229	.	-	.	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "2"; exon_id "NM_001099327.2"; gene_name "100043387";
chr2	refGene	exon	176086435	176086561	.	-	.	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "3"; exon_id "NM_001099327.3"; gene_name "100043387";
chr2	refGene	start_codon	176093582	176093584	.	-	0	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "1"; exon_id "NM_001099327.1"; gene_name "100043387";
chr2	refGene	exon	176093582	176093636	.	-	.	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "4"; exon_id "NM_001099327.4"; gene_name "100043387";
chr2	refGene	exon	176097100	176097171	.	-	.	gene_id "100043387"; transcript_id "NM_001099327"; exon_number "5"; exon_id "NM_001099327.5"; gene_name "100043387";
chr4	refGene	exon	41452042	41452201	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "1"; exon_id "NM_001048005.1"; gene_name "1110017D15Rik";
chr4	refGene	stop_codon	41452601	41452603	.	-	0	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "1"; exon_id "NM_001048005.1"; gene_name "1110017D15Rik";
chr4	refGene	exon	41452601	41452687	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "2"; exon_id "NM_001048005.2"; gene_name "1110017D15Rik";
chr4	refGene	exon	41454132	41454361	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "3"; exon_id "NM_001048005.3"; gene_name "1110017D15Rik";
chr4	refGene	exon	41454554	41454626	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "4"; exon_id "NM_001048005.4"; gene_name "1110017D15Rik";
chr4	refGene	exon	41455550	41455662	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "5"; exon_id "NM_001048005.5"; gene_name "1110017D15Rik";
chr4	refGene	exon	41458465	41458609	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "6"; exon_id "NM_001048005.6"; gene_name "1110017D15Rik";
chr4	refGene	exon	41464061	41464366	.	-	.	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "7"; exon_id "NM_001048005.7"; gene_name "1110017D15Rik";
chr4	refGene	start_codon	41464193	41464195	.	-	0	gene_id "1110017D15Rik"; transcript_id "NM_001048005"; exon_number "1"; exon_id "NM_001048005.1"; gene_name "1110017D15Rik";
chr10	refGene	exon	79635689	79635919	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	start_codon	79635711	79635713	.	+	0	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	exon	79636954	79637070	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "2"; exon_id "NM_027207.2"; gene_name "1600002K03Rik";
chr10	refGene	stop_codon	79637069	79637070	.	+	0	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	stop_codon	79637562	79637562	.	+	1	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	exon	79637562	79637864	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "3"; exon_id "NM_027207.3"; gene_name "1600002K03Rik";
chr7	refGene	exon	97273346	97273542	.	-	.	gene_id "2310010J17Rik"; transcript_id "NR_046007"; exon_number "1"; exon_id "NR_046007.1"; gene_name "2310010J17Rik";
chr7	refGene	exon	97275438	97275554	.	-	.	gene_id "2310010J17Rik"; transcript_id "NR_046007"; exon_number "2"; exon_id "NR_046007.2"; gene_name "2310010J17Rik";
chr7	refGene	exon	97278382	97278446	.	-	.	gene_id "2310010J17Rik"; transcript_id "NR_046007"; exon_number "3"; exon_id "NR_046007.3"; gene_name "2310010J17Rik";
chr16	refGene	start_codon	32271695	32271697	.	+	0	gene_id "2310010M20Rik"; transcript_id "NM_183283"; exon_number "1"; exon_id "NM_183283.1"; gene_name "2310010M20Rik";
chr16	refGene	exon	32271695	32271744	.	+	.	gene_id "2310010M20Rik"; transcript_id "NM_183283"; exon_number "1"; exon_id "NM_183283.1"; gene_name "2310010M20Rik";
chr16	refGene	exon	32273242	32273391	.	+	.	gene_id "2310010M20Rik"; transcript_id "NM_183283"; exon_number "2"; exon_id "NM_183283.2"; gene_name "2310010M20Rik";
chr16	refGene	exon	32273799	32274865	.	+	.	gene_id "2310010M20Rik"; transcript_id "NM_183283"; exon_number "3"; exon_id "NM_183283.3"; gene_name "2310010M20Rik";
chr16	refGene	stop_codon	32274241	32274243	.	+	0	gene_id "2310010M20Rik"; transcript_id "NM_183283"; exon_number "1"; exon_id "NM_183283.1"; gene_name "2310010M20Rik";


chr7	mm9_refGene	exon	147995576	147999213	0.000000	-	.	gene_id "NM_001001180"; transcript_id "NM_001001180"; 
chr7	mm9_refGene	stop_codon	147997328	147997330	0.000000	-	.	gene_id "NM_001001180"; transcript_id "NM_001001180"; 
chr7	mm9_refGene	exon	148004487	148004613	0.000000	-	.	gene_id "NM_001001180"; transcript_id "NM_001001180"; 
chr7	mm9_refGene	start_codon	148007934	148007936	0.000000	-	.	gene_id "NM_001001180"; transcript_id "NM_001001180"; 
chr7	mm9_refGene	exon	148007934	148008077	0.000000	-	.	gene_id "NM_001001180"; transcript_id "NM_001001180"; 
chr1	mm9_refGene	exon	58519615	58521134	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	stop_codon	58521048	58521050	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58522839	58522957	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58524495	58524556	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58526512	58526683	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58527784	58527930	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58529149	58529245	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58531653	58531785	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58533278	58533387	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58537095	58537193	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58537804	58537997	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58540487	58540547	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58549701	58549732	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58550505	58550594	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58554220	58554309	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	exon	58558167	58558270	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr1	mm9_refGene	start_codon	58558258	58558260	0.000000	-	.	gene_id "NM_001025378"; transcript_id "NM_001025378"; 
chr18	mm9_refGene	exon	48204989	48205099	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr18	mm9_refGene	exon	48206387	48208037	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr18	mm9_refGene	start_codon	48206411	48206413	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr18	mm9_refGene	stop_codon	48207713	48207715	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149611433	149611449	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149613582	149613675	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	start_codon	149613591	149613593	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149615154	149615249	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149616231	149616289	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149618114	149618183	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149618350	149618483	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149619224	149619446	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149620679	149620876	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149621560	149621761	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149621940	149622048	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149622170	149622228	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	exon	149622595	149622982	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr4	mm9_refGene	stop_codon	149622662	149622664	0.000000	+	.	gene_id "NM_001025388"; transcript_id "NM_001025388"; 
chr16	mm9_refGene	exon	26581791	26581972	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26624241	26624305	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	start_codon	26624242	26624244	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26676795	26677080	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26680189	26680375	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26692831	26692996	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26695308	26695379	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26698913	26699039	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26701174	26701322	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26710567	26710716	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26712203	26712346	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26722442	26723017	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	stop_codon	26723017	26723017	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	stop_codon	26723307	26723308	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr16	mm9_refGene	exon	26723307	26725233	0.000000	+	.	gene_id "NM_001159317"; transcript_id "NM_001159317"; 
chr1	mm9_refGene	exon	100317701	100318074	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	start_codon	100317783	100317785	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100319666	100319926	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100324843	100325028	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100328810	100328906	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100340205	100340323	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100343290	100343399	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100363235	100363379	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100377168	100377363	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100387074	100387227	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100392762	100392949	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100394054	100394118	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100396336	100396473	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	stop_codon	100396473	100396473	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	stop_codon	100405796	100405797	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chr1	mm9_refGene	exon	100405796	100405957	0.000000	+	.	gene_id "NM_001164233"; transcript_id "NM_001164233"; 
chrUn_random	mm9_refGene	exon	527839	528262	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	stop_codon	528232	528234	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	exon	528345	528527	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	exon	528622	528742	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	exon	528831	528969	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	start_codon	528895	528897	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	exon	41774207	41774345	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	start_codon	41774279	41774281	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	exon	41774434	41774554	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	exon	41774649	41774831	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	exon	41774914	41775337	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chr4	mm9_refGene	stop_codon	41774942	41774944	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666"; 
chrUn_random	mm9_refGene	exon	739163	739586	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chrUn_random	mm9_refGene	stop_codon	739556	739558	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chrUn_random	mm9_refGene	exon	739669	739851	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chrUn_random	mm9_refGene	exon	739946	740066	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chrUn_random	mm9_refGene	exon	740155	740293	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chrUn_random	mm9_refGene	start_codon	740219	740221	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	exon	41985510	41985648	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	start_codon	41985582	41985584	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	exon	41985737	41985857	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	exon	41985952	41986134	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	exon	41986217	41986640	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	stop_codon	41986245	41986247	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup1"; 
chr4	mm9_refGene	exon	42391950	42392373	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	stop_codon	42392343	42392345	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	exon	42392456	42392638	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	exon	42392733	42392853	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	exon	42392942	42393080	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	start_codon	42393006	42393008	0.000000	-	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup2"; 
chr4	mm9_refGene	exon	42625655	42625793	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chr4	mm9_refGene	start_codon	42625727	42625729	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chr4	mm9_refGene	exon	42625882	42626002	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chr4	mm9_refGene	exon	42626097	42626279	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chr4	mm9_refGene	exon	42626362	42626785	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chr4	mm9_refGene	stop_codon	42626390	42626392	0.000000	+	.	gene_id "NM_001193666"; transcript_id "NM_001193666_dup3"; 
chrUn_random	mm9_refGene	exon	1737773	1737846	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chrUn_random	mm9_refGene	exon	1738982	1739295	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chrUn_random	mm9_refGene	start_codon	1739009	1739011	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chrUn_random	mm9_refGene	exon	1739750	1740340	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chrUn_random	mm9_refGene	exon	1741238	1741852	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chrUn_random	mm9_refGene	stop_codon	1741803	1741805	0.000000	+	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	exon	94495480	94496094	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	stop_codon	94495527	94495529	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	exon	94496992	94497582	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	exon	94498037	94498350	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	start_codon	94498321	94498323	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	exon	94499498	94499571	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457"; 
chr5	mm9_refGene	exon	96161111	96161725	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr5	mm9_refGene	stop_codon	96161158	96161160	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr5	mm9_refGene	exon	96162623	96163213	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr5	mm9_refGene	exon	96163668	96163981	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr5	mm9_refGene	start_codon	96163952	96163954	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr5	mm9_refGene	exon	96165119	96165192	0.000000	-	.	gene_id "NM_001270457"; transcript_id "NM_001270457_dup1"; 
chr17	mm9_refGene	exon	31298341	31298538	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr17	mm9_refGene	stop_codon	31298522	31298524	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr17	mm9_refGene	exon	31299600	31299752	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr17	mm9_refGene	exon	31301872	31301998	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr17	mm9_refGene	start_codon	31301963	31301965	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr5	mm9_refGene	exon	143285577	143285774	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr5	mm9_refGene	stop_codon	143285758	143285760	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr5	mm9_refGene	exon	143286836	143286988	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr5	mm9_refGene	exon	143289108	143289234	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr5	mm9_refGene	start_codon	143289199	143289201	0.000000	-	.	gene_id "NM_009362"; transcript_id "NM_009362"; 
chr11	mm9_refGene	exon	68902030	68902129	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	start_codon	68902128	68902129	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	start_codon	68902608	68902608	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	exon	68902608	68902728	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	exon	68903233	68903391	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	exon	68903478	68903529	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	exon	68904152	68905883	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chr11	mm9_refGene	stop_codon	68904166	68904168	0.000000	+	.	gene_id "NM_009497"; transcript_id "NM_009497"; 
chrY	mm9_refGene	exon	155156	155257	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	start_codon	157264	157266	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	157264	157380	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	157495	157550	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	157635	157803	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	157893	158027	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	158589	158695	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	158902	158992	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	159587	159719	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	161891	161988	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	162085	162231	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	162342	162518	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	162621	162725	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	162814	162894	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	163205	163360	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	165209	165374	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	165584	165780	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	167702	167766	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	168018	168213	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	168767	168841	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	168947	169139	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	170618	170706	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	178411	178503	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	178623	178814	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	179367	179468	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	179577	179677	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	exon	179830	180667	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY	mm9_refGene	stop_codon	179963	179965	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43172478	43172579	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	start_codon	43174586	43174588	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43174586	43174702	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43174817	43174872	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43174957	43175125	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43175215	43175349	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43175911	43176017	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43176224	43176314	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43176909	43177041	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43179213	43179310	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43179407	43179553	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43179664	43179840	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43179943	43180047	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43180136	43180216	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43180527	43180682	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43182531	43182696	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43182906	43183102	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43185024	43185088	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43185340	43185535	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43186089	43186163	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43186269	43186461	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43187940	43188028	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43195733	43195825	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43195945	43196136	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43196689	43196790	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43196899	43196999	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	exon	43197152	43197989	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chrY_random	mm9_refGene	stop_codon	43197285	43197287	0.000000	+	.	gene_id "NM_011667"; transcript_id "NM_011667"; 
chr12	mm9_refGene	exon	31596534	31597092	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	start_codon	31597092	31597092	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	start_codon	31607100	31607101	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31607100	31607210	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31609629	31609742	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31611675	31611739	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31624439	31624551	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31625156	31625284	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31626832	31626994	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31627655	31627733	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31643713	31643769	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	exon	31644669	31645014	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr12	mm9_refGene	stop_codon	31644857	31644859	0.000000	+	.	gene_id "NM_013709"; transcript_id "NM_013709"; 
chr17_random	mm9_refGene	exon	581195	581311	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	600251	600446	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	start_codon	600275	600277	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	602234	602362	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	604618	604715	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	609590	609716	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	610273	610367	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	611771	611951	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	exon	612164	612733	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17_random	mm9_refGene	stop_codon	612274	612276	0.000000	+	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54100940	54101509	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	stop_codon	54101397	54101399	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54101722	54101902	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54103306	54103400	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54103957	54104083	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54108958	54109055	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54111311	54111439	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54113227	54113422	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	start_codon	54113396	54113398	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr17	mm9_refGene	exon	54129840	54129956	0.000000	-	.	gene_id "NM_018751"; transcript_id "NM_018751"; 
chr11	mm9_refGene	exon	79314484	79316529	0.000000	-	.	gene_id "NM_019409"; transcript_id "NM_019409"; 
chr11	mm9_refGene	stop_codon	79315201	79315203	0.000000	-	.	gene_id "NM_019409"; transcript_id "NM_019409"; 
chr11	mm9_refGene	start_codon	79317405	79317407	0.000000	-	.	gene_id "NM_019409"; transcript_id "NM_019409"; 
chr11	mm9_refGene	exon	79317405	79317584	0.000000	-	.	gene_id "NM_019409"; transcript_id "NM_019409"; 
chr10	mm9_refGene	exon	127496038	127496342	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	start_codon	127496341	127496342	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	start_codon	127505728	127505728	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127505728	127505841	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127506272	127506341	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127507190	127507288	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127509124	127509213	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127511278	127511340	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127512394	127512418	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	exon	127513123	127514310	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr10	mm9_refGene	stop_codon	127513140	127513142	0.000000	+	.	gene_id "NM_019766"; transcript_id "NM_019766"; 
chr17_random	mm9_refGene	exon	39677	41691	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	stop_codon	40445	40447	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	42329	42443	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	43007	43202	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	44596	44705	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	45129	45290	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	45800	45966	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	47141	47207	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	47495	47548	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	47638	47718	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	start_codon	47662	47664	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17_random	mm9_refGene	exon	48466	48574	0.000000	-	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8118865	8118973	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8119721	8119801	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	start_codon	8119775	8119777	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8119891	8119944	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8120232	8120298	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8121473	8121639	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8122149	8122310	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8122734	8122843	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8124237	8124432	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8124996	8125110	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	exon	8125748	8127762	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr17	mm9_refGene	stop_codon	8126992	8126994	0.000000	+	.	gene_id "NM_145968"; transcript_id "NM_145968"; 
chr3	mm9_refGene	exon	138868857	138868971	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	start_codon	138868863	138868865	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138875216	138875328	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138878222	138878350	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138881153	138881317	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138895162	138895274	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138906038	138906149	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138961369	138961476	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138969108	138969264	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138972046	138972206	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	138980356	138980445	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	139082669	139082828	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	139185822	139185940	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	139364589	139364737	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	stop_codon	139364736	139364737	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	stop_codon	139372137	139372137	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 
chr3	mm9_refGene	exon	139372137	139373263	0.000000	+	.	gene_id "NM_198659"; transcript_id "NM_198659"; 


chr10	refGene	exon	79635689	79635919	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	start_codon	79635711	79635713	.	+	0	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	exon	79636954	79637070	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "2"; exon_id "NM_027207.2"; gene_name "1600002K03Rik";
chr10	refGene	stop_codon	79637069	79637070	.	+	0	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	stop_codon	79637562	79637562	.	+	1	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "1"; exon_id "NM_027207.1"; gene_name "1600002K03Rik";
chr10	refGene	exon	79637562	79637864	.	+	.	gene_id "1600002K03Rik"; transcript_id "NM_027207"; exon_number "3"; exon_id "NM_027207.3"; gene_name "1600002K03Rik";
chr11	refGene	exon	110829347	110829409	.	+	.	gene_id "Kcnj16"; transcript_id "NM_001252207"; exon_number "1"; exon_id "NM_001252207.1"; gene_name "Kcnj16";
chr11	refGene	exon	110847744	110847824	.	+	.	gene_id "Kcnj16"; transcript_id "NM_001252207"; exon_number "2"; exon_id "NM_001252207.2"; gene_name "Kcnj16";
chr11	refGene	exon	110885723	110889281	.	+	.	gene_id "Kcnj16"; transcript_id "NM_001252207"; exon_number "3"; exon_id "NM_001252207.3"; gene_name "Kcnj16";
chr11	refGene	start_codon	110885828	110885830	.	+	0	gene_id "Kcnj16"; transcript_id "NM_001252207"; exon_number "1"; exon_id "NM_001252207.1"; gene_name "Kcnj16";
chr11	refGene	stop_codon	110887085	110887087	.	+	0	gene_id "Kcnj16"; transcript_id "NM_001252207"; exon_number "1"; exon_id "NM_001252207.1"; gene_name "Kcnj16";
chrY_random	refGene	exon	4246223	4247319	.	-	.	gene_id "LOC434960"; transcript_id "NM_001025241"; exon_number "1"; exon_id "NM_001025241.1"; gene_name "LOC434960";
chrY_random	refGene	stop_codon	4246355	4246357	.	-	0	gene_id "LOC434960"; transcript_id "NM_001025241"; exon_number "1"; exon_id "NM_001025241.1"; gene_name "LOC434960";
chrY_random	refGene	start_codon	4247036	4247038	.	-	0	gene_id "LOC434960"; transcript_id "NM_001025241"; exon_number "1"; exon_id "NM_001025241.1"; gene_name "LOC434960";
chrY_random	refGene	exon	4248546	4248568	.	-	.	gene_id "LOC434960"; transcript_id "NM_001025241"; exon_number "2"; exon_id "NM_001025241.2"; gene_name "LOC434960";
chrY_random	refGene	exon	52515006	52515028	.	+	.	gene_id "LOC434960"; transcript_id "NM_001025241_3"; exon_number "1"; exon_id "NM_001025241_3.1"; gene_name "LOC434960";
chrY_random	refGene	exon	52516257	52517353	.	+	.	gene_id "LOC434960"; transcript_id "NM_001025241_3"; exon_number "2"; exon_id "NM_001025241_3.2"; gene_name "LOC434960";
chrY_random	refGene	start_codon	52516538	52516540	.	+	0	gene_id "LOC434960"; transcript_id "NM_001025241_3"; exon_number "1"; exon_id "NM_001025241_3.1"; gene_name "LOC434960";
chrY_random	refGene	stop_codon	52517219	52517221	.	+	0	gene_id "LOC434960"; transcript_id "NM_001025241_3"; exon_number "1"; exon_id "NM_001025241_3.1"; gene_name "LOC434960";
chr10	refGene	exon	57857121	57857348	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "1"; exon_id "NM_001193303.1"; gene_name "Lims1";
chr10	refGene	start_codon	57857167	57857169	.	+	0	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "1"; exon_id "NM_001193303.1"; gene_name "Lims1";
chr10	refGene	exon	57861769	57861928	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "2"; exon_id "NM_001193303.2"; gene_name "Lims1";
chr10	refGene	exon	57870818	57870884	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "3"; exon_id "NM_001193303.3"; gene_name "Lims1";
chr10	refGene	exon	57872308	57872428	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "4"; exon_id "NM_001193303.4"; gene_name "Lims1";
chr10	refGene	exon	57872801	57872950	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "5"; exon_id "NM_001193303.5"; gene_name "Lims1";
chr10	refGene	exon	57875151	57875301	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "6"; exon_id "NM_001193303.6"; gene_name "Lims1";
chr10	refGene	exon	57876721	57876813	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "7"; exon_id "NM_001193303.7"; gene_name "Lims1";
chr10	refGene	exon	57879382	57879430	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "8"; exon_id "NM_001193303.8"; gene_name "Lims1";
chr10	refGene	exon	57881147	57881222	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "9"; exon_id "NM_001193303.9"; gene_name "Lims1";
chr10	refGene	exon	57881395	57881534	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "10"; exon_id "NM_001193303.10"; gene_name "Lims1";
chr10	refGene	stop_codon	57881534	57881534	.	+	0	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "1"; exon_id "NM_001193303.1"; gene_name "Lims1";
chr10	refGene	stop_codon	57884202	57884203	.	+	2	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "1"; exon_id "NM_001193303.1"; gene_name "Lims1";
chr10	refGene	exon	57884202	57887439	.	+	.	gene_id "Lims1"; transcript_id "NM_001193303"; exon_number "11"; exon_id "NM_001193303.11"; gene_name "Lims1";
chr1	refGene	exon	20880703	20880767	.	+	.	gene_id "Paqr8"; transcript_id "NM_028829"; exon_number "1"; exon_id "NM_028829.1"; gene_name "Paqr8";
chr1	refGene	exon	20922141	20922320	.	+	.	gene_id "Paqr8"; transcript_id "NM_028829"; exon_number "2"; exon_id "NM_028829.2"; gene_name "Paqr8";
chr1	refGene	exon	20924663	20928837	.	+	.	gene_id "Paqr8"; transcript_id "NM_028829"; exon_number "3"; exon_id "NM_028829.3"; gene_name "Paqr8";
chr1	refGene	start_codon	20924705	20924707	.	+	0	gene_id "Paqr8"; transcript_id "NM_028829"; exon_number "1"; exon_id "NM_028829.1"; gene_name "Paqr8";
chr1	refGene	stop_codon	20925767	20925769	.	+	0	gene_id "Paqr8"; transcript_id "NM_028829"; exon_number "1"; exon_id "NM_028829.1"; gene_name "Paqr8";
chr1	refGene	exon	9535489	9537536	.	+	.	gene_id "Rrs1"; transcript_id "NM_021511"; exon_number "1"; exon_id "NM_021511.1"; gene_name "Rrs1";
chr1	refGene	start_codon	9535605	9535607	.	+	0	gene_id "Rrs1"; transcript_id "NM_021511"; exon_number "1"; exon_id "NM_021511.1"; gene_name "Rrs1";
chr1	refGene	stop_codon	9536700	9536702	.	+	0	gene_id "Rrs1"; transcript_id "NM_021511"; exon_number "1"; exon_id "NM_021511.1"; gene_name "Rrs1";
chr1	refGene	exon	157882857	157883050	.	+	.	gene_id "Tor1aip2"; transcript_id "NM_001160180"; exon_number "1"; exon_id "NM_001160180.1"; gene_name "Tor1aip2";
chr1	refGene	exon	157888205	157888264	.	+	.	gene_id "Tor1aip2"; transcript_id "NM_001160180"; exon_number "2"; exon_id "NM_001160180.2"; gene_name "Tor1aip2";
chr1	refGene	exon	157898424	157900866	.	+	.	gene_id "Tor1aip2"; transcript_id "NM_001160180"; exon_number "3"; exon_id "NM_001160180.3"; gene_name "Tor1aip2";
chr1	refGene	start_codon	157899008	157899010	.	+	0	gene_id "Tor1aip2"; transcript_id "NM_001160180"; exon_number "1"; exon_id "NM_001160180.1"; gene_name "Tor1aip2";
chr1	refGene	stop_codon	157899401	157899403	.	+	0	gene_id "Tor1aip2"; transcript_id "NM_001160180"; exon_number "1"; exon_id "NM_001160180.1"; gene_name "Tor1aip2";
</pre>
