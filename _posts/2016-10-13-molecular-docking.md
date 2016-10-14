---
title: Basic molecular docking
author: ct
layout: post
categories:
  - Docking
tags:
  - Docking
---

### Molecular Docking理论



### 蛋白可视化

我们观察的是一个分辨率为2艾的X-射线衍射晶体结构(PDB ID: [1HSG](http://www.rcsb.org/pdb/explore/explore.do?structureId=1HSG))，展示的是HIV-1蛋白酶与药物茚地那韦([indinavir](http://en.wikipedia.org/wiki/Indinavir))结合在一起的构象。软件[`PyMOL`](https://pymolwiki.org/index.php/Practical_Pymol_for_Beginners)用来观察HIV-蛋白酶、结合位点和药物分析的结构。

* 下载HIV-1蛋白酶的PDB结构(https://files.rcsb.org/download/1HSG.pdb)，存储到一个不含中文的目录下。
* 启动PyMOL
* 选择`File`-`Open`-`1hsg.pdb`

![file_open_visual.png]({{ site.imgurl }}/docking/file_open_visual.png)

* 首先隐藏所有的图像，在右侧的对象控制面板，行`all`的`H`列`Hide: everything`，这时屏幕应该是漆黑一片。

![all_hide_everything.png]({{ site.imgurl }}/docking/all_hide_everything.png)

* 显示蛋白，在右侧的对象控制面板，行`1hsg`的`S`列，选择`cartoon`展示，然后在`C`列按`chain`显色，这时可以看到一个同源二聚体的展示。

![1hsg_cartoon_chain.png]({{ site.imgurl }}/docking/1hsg_cartoon_chain.png)

* 显色配体药物`indinavir`，其残基的名字为`MK1`,这个信息可以在上述PDB网站链接查看，具体如下图所示。

![ligand_indinavir_mk1.png]({{ site.imgurl }}/docking/ligand_indinavir_mk1.png)

在PyMOL的命令行处输入`select indinavir, resn MK1`，如下图所示

![get_ligand_using_select.png]({{ site.imgurl }}/docking/get_ligand_using_select.png)

回车后，会看到界面如图所示

![ligand_indinavir_mk1_show_1.png]({{ site.imgurl }}/docking/ligand_indinavir_mk1_show_1.png)

* 显示配体，在右侧的对象控制面板，行`indinavir`的`S`列，选择`stick`展示，再选择`C`一种不同的颜色。在屏幕没有无图处点击鼠标，取消选择。

![lgand_show.png]({{ site.imgurl }}/docking/lgand_show.png)

* PyMOL鼠标操作：按住左键移动旋转，按住右键移动放大，按住中键移动，观察结合位点所在的位置。

* 显示水分子，水分子的残基名字为`HOH`，运行命令`select H2O, resn HOH`调出水分子。然后选择`S`-`spheres`,`C`-`red`。再运行`set sphere_scale, 0.2`设置水球的大小。

* 存储, 在命令行输入`png E:/docking/1shg.png`保存当前结果。

![1hsg.png]({{ site.imturl }}/docking/1hsg.png)

### 准备docking需要的受体(protein)和配体(化合物)

Docking算法需要每个原子带有电荷并且需要标记原子的属性。这些信息在PDB文件中不存在。我们需要在生成一个[`PDBQT`](http://autodock.scripps.edu/faqs-help/faq/what-is-the-format-of-a-pdbqt-file)文件包含以上信息和PDB文件中的原子坐标信息。进一步地对于“柔性配体docking”，我们还需要定义配体的哪些键是可以旋转的。所有这些都可以通过软件[`AutoDock Tools (adt)`](http://mgltools.scripps.edu/)来完成。

Docking algorithms require each atom to have a charge and an atom type that describes its properties. However, the PDB structure lacks these. So, we have to prep the protein and ligand files to include these values along with the atomic coordinates. Furthermore, for flexible ligand docking, we should also define ligand bonds that are rotatable. All this will be done in a tool called AutoDock Tools (adt).

#### 准备受体蛋白

1. PDB文件(1hsg.pdb)中包含了蛋白、配体和水分子；首先提取出蛋白的坐标，即以关键字`ATOM`开头的行。每一条蛋白链以关键字`TER`开头的行作为终止行。

  * 在windows下，我们可以手动选择，或者利用Excel的筛选功能。
  * 在Linux下，使用命令`egrep "^(ATOM|TER)"` 1hsg.pdb >1hsg_prot.pdb

2. 启动AutoDockTools
  
  * windows直接双击图标就可
  * linux可以使用命令`adt &`

3. 加载蛋白分子 `File`-`Read MOlecule`-'1hsg_prot.pdb'。
  
  * ADT中按住左键拖动旋转分子结构；点击中键，滚动缩放；按住邮件移动晶体位置。

4. 更改展示方式，`Color`-`By Atom Type`-`All Geometries`-`OK`。

5. 晶体结构中通常缺少氢原子 (因为氢原子电子少，且质子核对电子吸引能力弱，因此很难定位，具体见<http://www.uh.edu/~chembi/ChemSocRev_Jones_critical.pdf>)。但是在docking过程中，氢原子，尤其是极性氢原子对计算静电作用是必须的。因此我们需要给蛋白加上氢原子，`Edit`-`Hydrogen`-`Add`-`Polar only`-`OK`(之所以选择`Polar only`是因为`vina`的官方视频里面是这么选择的)。这时氢原子会以白色短线形式出现。

<figure class="half">
	<img src="{{ site.imgurl }}/docking/1hsg_prot_no_H.png" alt="1hsg_prot_no_H.png">
	<img src="{{ site.imgurl }}/docking/1hsg_prot_with_H.png" alt="1hsg_prot_with_H.png">
	<figcaption>增加氢原子前（左）和后（右）蛋白结构显示</figcaption>
</figure>

6. 存储对蛋白的每个原子所做的修改和原子类型，`Grid`-`Macromolecule`-`Choose`,选择`1HSG_protein`-`Slect Molecule`。ADT会合并非极性氢原子，实施改变并提示保存`Save`-`1hsg_prot.pdbqt`。打开文件，查看最后两列，分别为每个原子的电量和类型。
  
  * `1hsg_prot.pdbqt`为只加了极性氢的结果
  * `1hsg_prot_all_h.pdbqt`为加了所以氢的结果
  
  这两个文件电量会有所不同，随后会测试它们对docking的影响，会发现没有影响，最后输出的日子文件一模一样。

7. 在受体上定义配体结合的3D搜索空间。如果我们事先不知道结合位点，我们可以定义一个盒子包含整个蛋白或者随便一个特定区域。`Grid`-`Grid box`将会在蛋白上画出一个长方体，并且有一个弹出框。在弹出框中，拖拽刻度线查看长方体的变化。

在这个例子中，我们知道结合位点，就选取以其为中心的一个小空间。设置`Spacing (angstrom)`为`1`埃 (这实际是一个换算系数)。在我们调整的过程中，可以看到随着这个数值的变大，立方体也被放大了。另外我们设置`x,y,z center`为`16,25,4`,`number of points in (x,y,z)-dimension`为`30,30,30`。记下我们设置的这些点。

关掉grid和protein：`Grid Options`-`File`-`Close w/out saving`; `Edit`-`Delete`-`Delete Molecule`-`1hsg_prot`-`Continue`。

#### 准备配体

1. 与蛋白结构类似，配体的结构也缺少氢原子，我们需要添加氢原子并且定义哪些键是可以旋转的以用于柔性docking。

2. 从PDB结构中提取配体的原子位置。`indinavir`的配体残基名字为`MK1`；以`HETATM`开头的行表示杂原子 (heteroatoms)。

  * Linux系统下，运行`grep "^HETATM.*MK1" 1hsg.pdb >indinavir.pdb`
  * Windows系统下，直接拷贝

3. 将结构读入ADT；`File`-`Read Molecule`-`indinavir.pdb`;`Color`-`By Atom Type`-`All Geometreies`-`OK`。

4. 晶体结构中通常缺少氢原子 (因为氢原子电子少，且质子核对电子吸引能力弱，因此很难定位，具体见<http://www.uh.edu/~chembi/ChemSocRev_Jones_critical.pdf>)。但是在docking过程中，氢原子，尤其是极性氢原子对计算静电作用是必须的。因此我们需要给配体加上氢原子，`Edit`-`Hydrogen`-`Add`-`Polar only`-`OK`(之所以选择`Polar only`是因为`vina`的官方视频里面是这么选择的)。这时氢原子会以白色短线形式出现。

<figure class="half">
	<img src="{{ site.imgurl }}/docking/indinavir_no_H.png" alt="1hsg_prot_no_H.png">
	<img src="{{ site.imgurl }}/docking/indinavir_with_H.png" alt="1hsg_prot_with_H.png">
	<figcaption>增加氢原子前（左）和后（右）化合物结构显示</figcaption>
</figure>

5. 在ADT中定义此化合物为配体，以便ADT为其计算局部电荷(partial charges)和设置可旋转配体键。`Ligand`-`input`-`Choose`-`indinavir`-`Select Molecule for AutoDock4`。这时会有一个弹出框指示ADT所做的操作，包括合并非极性氢（只在添加了的情况下）、计算电荷电量和设置旋转键。然后存储结果`Ligand`-`Output`-`Save as PDBQT`。

  * `indinavir.pdbqt`为只加了极性氢的结果
  * `indinavir_all_h.pdbqt`为加了所以氢的结果

查看ADT检测出的旋转键，`Ligand`-`Torsion Tree`-`Choose Torsions`,可以看到`Number of rotatable bonds=14/32`。

输出配体的pdbqt问题，`Lignad`-`Output`-`Dave as PDBQT`

#### 准备docking配置文件

docking配置文件包含了输入的受体（蛋白）、配体（化合物）和搜索参数的信息，为一个文本文件，名字任意，可以为`conf.txt`，内容如下

```
receptor = 1hsg_prot.pdbqt
ligand   = indinavir.pdbqt

num_modes = 50

out = dockingResult.pdbqt
log = docking.log

center_x = 16
center_y = 25
center_z = 4

size_x = 30
size_y = 30
size_z = 30

seed = 2009
```

### Docking indinavir到HIV-1蛋白酶

1. 使用[`AutoDock Vina`](http://vina.scripps.edu/)执行docking预测。

2. 在windows命令行提示符或linux终端下运行命令 `vina --config conf.txt`，运行几分钟。

3. 运行的输出包含两个文件，结果文件`dockingResult.pdbqt`和日志文件`docking.log`。
  * `dockingResult.pdbqt`: 包含所有docking的模式，第一个为结合最好的构象
  * `docking.log`: 日志文件，包含结合能量值（第一列，越低越稳定，第一个为最好的构象）、每个构象与第一个构象的距离、每个构象与第一个构象的差别。
    
	```
    Detected 4 CPUs
    Reading input ... done.
    Setting up the scoring function ... done.
    Analyzing the binding site ... done.
    Using random seed: 2009
    Performing search ... done.
    Refining results ... done.
    
    mode |   affinity | dist from best mode
         | (kcal/mol) | rmsd l.b.| rmsd u.b.
    -----+------------+----------+----------
       1        -11.5      0.000      0.000
       2        -10.6      1.425      4.304
       3        -10.4      2.042     10.990
       4        -10.3      2.034     10.326
	```

4. 用`PyMOL`可视化docking结果

`File`-`Open`文件类型选择`All FIles`-选取结果`pdbqt文件`、`原始蛋白和配体的pdb文件`、`原教程的pdbqt文件`。
  
  * dockingResult.pdbqt: 增加非极性氢的docking结果
  * dockingResultAllH.pdbqt: 增加所有氢的docking结果
  * original_tutorial_result.pdbqt：原教程中的docking结果

<figure class="third">
	<img src="{{ site.imgurl }}/docking/docking_result_all.png" alt="docking_result_all.png">
	<img src="{{ site.imgurl }}/docking/our_ligand_gold_standard.png" alt="our_ligand_gold_standard.png">
	<img src="{{ site.imgurl }}/docking/our_ligand_original_ligand.png" alt="our_ligand_original_ligand.png">
	<figcaption>Docking结果展示。白色化合物为原PDB晶体结构中配体的构象，视为金标准。蓝色为本教程的结果只加极性氢。粉红色为原教程结果。黄色为本教程加所有氢的结果 (与蓝色构象完全一致，因此显示不出)。</figcaption>
</figure>

### Docking非原生配体

在前面的例子中，`AutoDock Vina`能把配体dock到几乎原生的构象。下面，我们尝试另外一个配体药物[`nelfinavir奈非那韦`](http://en.wikipedia.org/wiki/Nelfinavir)，来展示如何寻找小分子在蛋白内的结合位点。这个过程可以进一步地凝练和扩展已作为“虚拟筛选(virtual screening)”的步骤。

* 在网站<https://pubchem.ncbi.nlm.nih.gov/compound/64143#section=3D-Conformer>获得其3D构象，下载`SDF`格式的文件。

* 在网站<http://www.drugbank.ca/drugs/DB00220>获得`PDB`格式的文件。
  * DB00220_nelfinavir.pdb：为我下载的pdb文件,是一个平面PDB结构。
  * nelfinavir.pdb：为教程提供的pdb文件

* 按照上述步骤对配体文件进行预处理获得`pdbqt`格式文件。

* 修改配置文件，执行Docking。

* 用`pymol`可视化结果。

* 对这个例子来讲，PDB中存在nelfinavir与HIV-1蛋白酶的晶体结构([1OHR](http://www.rcsb.org/pdb/explore/explore.do?structureId=1OHR))，可以作为金标准来检测docking的准确性。

* pymol中导入`1OHR.pdb`文件，在对象面板的`1OHR`行，点击`H`-`hide everything`，点击`S`-`show cartoons`，`C`-`By chain`。从图中可以看到这两个蛋白酶体在空间的方向不同，因此我们需要重新比对这两个结构,`PyMOL> align 1OHR, 1hsg_prot`，可以看到两个结构完全重合了。

You may have observed that moving the structure around the window is a bit difficult since the origin of the view has been altered when you loaded 1OHR.pdb. To reset it, try:`PyMOL> reset`，运行之后没有看到变化。

提取`1OHR`中的`nelfinavir (残基为1UN)`,`PyMOL> select nelfinavir, 1OHR and resn 1UN`，对象面板更改其展示方式，`S`-`sticks`, `C`-`white`。

<figure class="half">
	<img src="{{ site.imgurl }}/docking/1OHR_1HSG_unalign.png" alt="1OHR_1HSG_unalign.png">
	<img src="{{ site.imgurl }}/docking/1OHR_1HSG_align.png" alt="1OHR_1HSG_align.png">
	<figcaption>Docking结果展示。第一张图表示2个晶体结构align前的展示；第二张图表示2个晶体align后重合在了一起。白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的结果(只加极性氢)。</figcaption>
</figure>

通过与金标准比对，判断哪个构象是预测的最佳模式。

<figure class="half">
	<img src="{{ site.imgurl }}/docking/nelfinavir_first_with_gold_standard.png" alt="nelfinavir_first_with_gold_standard.png">
	<img src="{{ site.imgurl }}/docking/nelfinavir_second_with_gold_standard.png" alt="nelfinavir_second_with_gold_standard.png">
	<figcaption>Docking第一张图表示AutoDock Vina输出结果的Best Mode与金标准的比对情况；第二张图表示AutoDock Vina输出结果的Second Best Mode与金标准的比对情况；白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的结果(只加极性氢)。</figcaption>
</figure>

结果看到`second best mode`看上去吻合的更好，为什么呢？从日志的结合能量来看，`best mode`和`second best mode`只差了0.2。

那么还有一个问题，1SHG的chainA与1OHR的chainA是不是一个呢？我们比对1OHR的chainA与1HSG的chainB，`PyMOL> align 1OHR and chain A, 1hsg_prot and chain B`。

<figure class="half">
	<img src="{{ site.imgurl }}/docking/1OHR_1HSG_chainA_align.png" alt="1OHR_1HSG_chainA_align.png">
	<img src="{{ site.imgurl }}/docking/1OHR_1HSG_chainAB_align.png" alt="1OHR_1HSG_chainAB_align.png">
	<figcaption>Docking结果展示。第一张图表示2个晶体结构align后重合在了一起。第二张图表示1OHR的chainA与1HSG的chainB比对的结果。白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的预测的second best mode结果(只加极性氢)。</figcaption>
</figure>

### 在蛋白表明搭建静电层 (electrostatic surface)

静电作用在分子docking过程中发挥着重要的作用。我们接下来将观察静电力是如何与配体作用的。

前面我们提到，PDB结构中不包含原子的局部电荷信息，而这对静电力场的计算是很重要的。因此我们需要给PDB文件中增加这一数据。






### 参考

* Detailed tutorial <http://sbcb.bioch.ox.ac.uk/users/greg/teaching/docking-2012.html>
* 官方文档 <http://vina.scripps.edu>
* PyMOL操作手册 <https://pymolwiki.org/index.php/Practical_Pymol_for_Beginners>
