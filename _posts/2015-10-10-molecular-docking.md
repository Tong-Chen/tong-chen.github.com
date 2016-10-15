---
title: Basic molecular docking
author: ct
layout: post
categories: [Docking]
tags: [Docking]
---

### Molecular Docking理论

AutoDock Vina使用拉马克遗传算法执行格点(grid)计算。首先在受体活性氨基酸附近划定一个长方体区域作为搜索空间，扫描不同类型的原子计算格点能量，在搜索空间内，调整配体的构象、位置和方向，进而评分、排序获得能量最低的构象作为输出结果。


### 蛋白可视化

例子文件是一个分辨率为2艾的X-射线衍射晶体结构(PDB ID: [1HSG](http://www.rcsb.org/pdb/explore/explore.do?structureId=1HSG))，其为HIV-1蛋白酶与药物茚地那韦([indinavir](http://en.wikipedia.org/wiki/Indinavir))结合在一起的构象。软件[`PyMOL`](https://pymolwiki.org/index.php/Practical_Pymol_for_Beginners)用来观察HIV-蛋白酶、结合位点和药物分子的结构。

* 下载HIV-1蛋白酶的PDB结构(<https://files.rcsb.org/download/1HSG.pdb>)，存储到一个不含中文和空格的目录下。
* 启动PyMOL，依次点选`File`-`Open`-`1hsg.pdb`，会看到如下界面

  ![file_open_visual.png]({{ site.img_url }}/docking/file_open_visual.png)

* 首先隐藏所有的图像，在右侧的对象控制面板，行`all`的`H`列`Hide: everything`，这时屏幕应该是漆黑一片。

![all_hide_everything.png]({{ site.img_url }}/docking/all_hide_everything.png)

* 显示蛋白，在右侧的对象控制面板，行`1hsg`的`S`列，选择`cartoon`展示，然后在`C`列按`chain`显色，这时可以看到一个同源二聚体的展示。

![1hsg_cartoon_chain.png]({{ site.img_url }}/docking/1hsg_cartoon_chain.png)

* 显色配体药物`indinavir`，其残基的名字为`MK1`,这个信息可以在上述PDB网站链接查看，具体如下图所示。

![ligand_indinavir_mk1.png]({{ site.img_url }}/docking/ligand_indinavir_mk1.png)

在PyMOL的命令行处输入`PyMOL> select indinavir, resn MK1`，回车，会看到
如下画面变化。

<figure class="half">
	<img src="{{ site.img_url }}/docking/get_ligand_using_select.png" alt="get_ligand_using_select.png">
	<img src="{{ site.img_url }}/docking/ligand_indinavir_mk1_show_1.png" alt="ligand_indinavir_mk1_show_1.png">
	<figcaption>左图展示输入的命令和输入命令前的结构图，右图展示输入命令后的结构图。</figcaption>
</figure>

* 显示配体，在右侧的对象控制面板，行`indinavir`的`S`列，选择`stick`展示，再选择`C`一种不同的颜色。在屏幕没有无图处点击鼠标，取消选择。

![lgand_show.png]({{ site.img_url }}/docking/lgand_show.png)

* PyMOL鼠标操作：按住左键移动旋转，按住右键移动放大，按住中键移动，观察结合位点所在的位置。

* 显示水分子，水分子的残基名字为`HOH`，运行命令`PyMOL> select H2O, resn HOH`调出水分子。然后选择`S`-`spheres`,`C`-`red`。再运行`set sphere_scale, 0.2`设置水球的大小。

* 存储, 在命令行输入`png E:/docking/1shg.png`保存当前结果。


![1hsg.png]({{ site.img_url }}/docking/1hsg.png)

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
	<img src="{{ site.img_url }}/docking/1hsg_prot_no_H.png" alt="1hsg_prot_no_H.png">
	<img src="{{ site.img_url }}/docking/1hsg_prot_with_H.png" alt="1hsg_prot_with_H.png">
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
	<img src="{{ site.img_url }}/docking/indinavir_no_H.png" alt="1hsg_prot_no_H.png">
	<img src="{{ site.img_url }}/docking/indinavir_with_H.png" alt="1hsg_prot_with_H.png">
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
       5        -10.2      2.517      4.774
       6        -10.1      1.933     10.911
       7         -9.9      2.176     10.884
       8         -9.8      1.794      3.600
       9         -9.6      1.981     10.865
      10         -9.5      2.431     10.943
      11         -9.3      2.417     10.370
      12         -8.9      2.404     10.285
      13         -8.8      4.058     10.904
      14         -8.7      5.574     11.291
      15         -8.7      4.441      8.312
      16         -8.6      5.659      8.929
      17         -8.6      4.404      8.275
      18         -8.5      5.630      8.900
    Writing output ... done.
	```

4. 用`PyMOL`可视化docking结果

`File`-`Open`文件类型选择`All FIles`-选取结果`pdbqt文件`、`原始蛋白和配体的pdb文件`、`原教程的pdbqt文件`。
  
  * dockingResult.pdbqt: 增加非极性氢的docking结果
  * dockingResultAllH.pdbqt: 增加所有氢的docking结果
  * original_tutorial_result.pdbqt：原教程中的docking结果

<figure class="third">
	<img src="{{ site.img_url }}/docking/docking_result_all.png" alt="docking_result_all.png">
	<img src="{{ site.img_url }}/docking/our_ligand_gold_standard.png" alt="our_ligand_gold_standard.png">
	<img src="{{ site.img_url }}/docking/our_ligand_original_ligand.png" alt="our_ligand_original_ligand.png">
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
     1        -11.2      0.000      0.000
     2        -11.0      1.878      9.618
     3         -9.8      1.354      4.254
     4         -9.6      1.732      8.679
     5         -9.5      1.192      1.814
     6         -9.2      1.669      2.269
     7         -9.0      2.003      8.075
     8         -8.7      1.850      3.803
     9         -8.4      1.856      9.549
  Writing output ... done.
  ```

* 用`pymol`可视化结果。

* 对这个例子来讲，PDB中存在nelfinavir与HIV-1蛋白酶的晶体结构([1OHR](http://www.rcsb.org/pdb/explore/explore.do?structureId=1OHR))，可以作为金标准来检测docking的准确性。

* pymol中导入`1OHR.pdb`文件，在对象面板的`1OHR`行，点击`H`-`hide everything`，点击`S`-`show cartoons`，`C`-`By chain`。从图中可以看到这两个蛋白酶体在空间的方向不同，因此我们需要重新比对这两个结构,`PyMOL> align 1OHR, 1hsg_prot`，可以看到两个结构完全重合了。

You may have observed that moving the structure around the window is a bit difficult since the origin of the view has been altered when you loaded 1OHR.pdb. To reset it, try:`PyMOL> reset`，运行之后没有看到变化。

提取`1OHR`中的`nelfinavir (残基为1UN)`,`PyMOL> select nelfinavir, 1OHR and resn 1UN`，对象面板更改其展示方式，`S`-`sticks`, `C`-`white`。

<figure class="half">
	<img src="{{ site.img_url }}/docking/1OHR_1HSG_unalign.png" alt="1OHR_1HSG_unalign.png">
	<img src="{{ site.img_url }}/docking/1OHR_1HSG_align.png" alt="1OHR_1HSG_align.png">
	<figcaption>Docking结果展示。第一张图表示2个晶体结构align前的展示；第二张图表示2个晶体align后重合在了一起。白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的结果(只加极性氢)。</figcaption>
</figure>

通过与金标准比对，判断哪个构象是预测的最佳模式。

<figure class="half">
	<img src="{{ site.img_url }}/docking/nelfinavir_first_with_gold_standard.png" alt="nelfinavir_first_with_gold_standard.png">
	<img src="{{ site.img_url }}/docking/nelfinavir_second_with_gold_standard.png" alt="nelfinavir_second_with_gold_standard.png">
	<figcaption>Docking第一张图表示AutoDock Vina输出结果的Best Mode与金标准的比对情况；第二张图表示AutoDock Vina输出结果的Second Best Mode与金标准的比对情况；白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的结果(只加极性氢)。</figcaption>
</figure>

结果看到`second best mode`看上去吻合的更好，为什么呢？从日志的结合能量来看，`best mode`和`second best mode`只差了0.2。

那么还有一个问题，1SHG的chainA与1OHR的chainA是不是一个呢？我们比对1OHR的chainA与1HSG的chainB，`PyMOL> align 1OHR and chain A, 1hsg_prot and chain B`。

<figure class="half">
	<img src="{{ site.img_url }}/docking/1OHR_1HSG_chainA_align.png" alt="1OHR_1HSG_chainA_align.png">
	<img src="{{ site.img_url }}/docking/1OHR_1HSG_chainAB_align.png" alt="1OHR_1HSG_chainAB_align.png">
	<figcaption>Docking结果展示。第一张图表示2个晶体结构align后重合在了一起。第二张图表示1OHR的chainA与1HSG的chainB比对的结果。白色化合物为1OHR PDB晶体结构中配体nelfinavir的构象，视为金标准。红色为本教程的预测的second best mode结果(只加极性氢)。</figcaption>
</figure>

### 在蛋白表明搭建静电层 (electrostatic surface)

静电作用在分子docking过程中发挥着重要的作用。我们接下来将观察静电力是如何与配体作用的。

前面我们提到，PDB结构中不包含原子的局部电荷信息，而这对静电力场的计算是很重要的。因此我们需要给PDB文件中增加这一数据。

为了完成这一任务，我们需要在<http://www.poissonboltzmann.org/>注册，然
后下载安装软件
[`APBS`](https://sourceforge.net/projects/apbs/)和
[`pdb2pqr`](https://sourceforge.net/projects/pdb2pqr/)。

* 在Windows下, `APBS`直接下载安装就可, 使用默认的安装目录；
  `pdb2pqr`解压缩到`C:\pdb2pqr`; 路径中不能有空格。

  设置环境变量：`我的电脑`-`属性`-`高级系统设置`-`高级`-`环境变量`-`系
  统变量中选中PATH`-`编辑`-`新建`-`加入安装路径(如下图所示)`

  ![windows_PATH.png]({{ site.img_url }}/docking/windows_PATH.png)

  安装完成之后，启动PyMOL，会在`Plugin`下看到`APBS Tools`。

* 在Lunux下，尚未试验。


打开PyMOL并读入`1hsg_prot.pdb`，然后通过下述步骤启动并配置APBS，
依次点击菜单或按钮，`Plugin` - `APBS Tools` - `Main` - 
`Select Use PyMOL generated PQR and
PyMOL generated Hydrogens and termini`(这步操作是给PDB文件中的每个原子
加氢、局部电荷和计算原子半径;This adds hydrogens and assigns
partial charges and atomic radii to each atom in the PDB file.) - 
`Configuration` - `Set grid`(点击后定义了一个保护蛋白的框，但并未显示
，因此点击后看不到任何反应。This defines a grid that encloses the
protein, but Grid is not displayed on the screen) - `System
Temperature = 300` - `on concentration (+1) and (-1) to 0.15`(相当于
0.15摩尔的阳离子和阴离子。which is equivalent of 0.15M cations and anions) 
- 按图设置APBS和pdb2pqr的路径 -  `Run APBS` - `Visualization` -
`Update`(如果出现*Unable to open file error*，运行命令`PyMOL > load
C:\Users\ct\AppData\Local\Temp\pymol-generated.dx`) - `Molecular
Surface - Show`

<figure class="third">
	<img src="{{ site.img_url }}/docking/pymol_apbs_config_1.png" alt="">
	<img src="{{ site.img_url }}/docking/pymol_apbs_config_2.png" alt="">
	<img src="{{ site.img_url }}/docking/pymol_apbs_config_location.png" alt="">
	<figcaption>左图为配置加氢的参数；中图是设置GRID；右图为设置可执行
	文件的路径</figcaption>
</figure>

<figure class="third">
	<img src="{{ site.img_url }}/docking/pymol_apbs_config_3.png" alt="">
	<img src="{{ site.img_url }}/docking/pymol_apbs_config_4.png" alt="">
	<img src="{{ site.img_url }}/docking/pymol_apbs_show.png" alt="">
	<figcaption>左图是展示APBS计算结果；中图为计算结果路径；右图为结果
	展示</figcaption>
</figure>






### 文件格式解释

PDB文件 [(详细格式描述)](http://www.wwpdb.org/documentation/file-format-content/format33/v3.3.html)

基本信息部分

* `HEADER`记录: 包括分子的分类、提交日期、PDB ID
* `TITLE`记录: 为该结构的描述，如果有多行，除第一行外，其它行有连续的数字标示。
* `COMPND`记录: 包含分子数目、名字、链特征、分子是如何获得的等。 
* `SOURCE`记录: 大分子的生物或化学来源
* `KEYWDS`记录：关键字
* `EXPDTA`记录：实验信息
* `JRNL`记录：文献引用信息 
* `REMARK`记录：更为丰富的记录信息


```
HEADER    HYDROLASE (ACID PROTEINASE)             31-MAR-95   1HSG              
TITLE     CRYSTAL STRUCTURE AT 1.9 ANGSTROMS RESOLUTION OF HUMAN                
TITLE    2 IMMUNODEFICIENCY VIRUS (HIV) II PROTEASE COMPLEXED WITH L-           
COMPND    MOL_ID: 1;                                                            
COMPND   2 MOLECULE: HIV-1 PROTEASE;                                            
COMPND   3 CHAIN: A, B;                                                         
COMPND   5 ENGINEERED: YES;                                                     
COMPND   6 OTHER_DETAILS: NY5 ISOLATE                                           
SOURCE    MOL_ID: 1;                                                            
SOURCE   2 ORGANISM_SCIENTIFIC: HUMAN IMMUNODEFICIENCY VIRUS 1;                 
SOURCE   6 EXPRESSION_SYSTEM_TAXID: 562                                         
KEYWDS    HYDROLASE (ACID PROTEINASE)                                           
EXPDTA    X-RAY DIFFRACTION                                                     
AUTHOR    Z.CHEN                                                                
REVDAT   3   24-FEB-09 1HSG    1       VERSN                                    
REVDAT   1   03-APR-96 1HSG    0                                                
JRNL        AUTH   Z.CHEN,Y.LI,E.CHEN,D.L.HALL,P.L.DARKE,C.CULBERSON,           
JRNL        TITL   CRYSTAL STRUCTURE AT 1.9-A RESOLUTION OF HUMAN               
JRNL        TITL 2 IMMUNODEFICIENCY VIRUS (HIV) II PROTEASE COMPLEXED           
JRNL        REF    J.BIOL.CHEM.                  V. 269 26344 1994              
JRNL        PMID   7929352                                                      
REMARK   1                                                                      
REMARK   3   PROGRAM     : X-PLOR                                               
REMARK   3   AUTHORS     : BRUNGER                                              
REMARK   3                                                                      
REMARK   3  DATA USED IN REFINEMENT.                                            
REMARK   3   RESOLUTION RANGE HIGH (ANGSTROMS) : 2.00                           
REMARK 800 SITE_DESCRIPTION: BINDING SITE FOR RESIDUE MK1 B 902                 
```

结构部分

* `DBREF`: 数据库的交叉引用信息
* `SEQRES`: 形成多聚合物的线性共价相连的化学组分
* `HET`: 表述提供了坐标的非标准残基，比如辅基、抑制子、溶剂分子和离子, 
  第二列如`MK1`为hetID, 可用于在pymol中提取信息展示`select name, resn hetID`。
* `FORMUL`：表述非标准聚合物外其它成分的化学结构，包括水(用*表示)。
  第二列如`MK1`为hetID, 可用于在pymol中提取信息展示`select H2O, resn HOH`。
* `HELIX`: 标记分子二级结构中螺旋的位置
* `SHEET`: 标记分子二级结构中片的位置
* `SITE`: 标示特殊残基，比如催化位点、辅因子、反密码子、调节位点或其它
  关键位点，也可标示配体的环境信息。这个信息对我们做Docking很重要，随
  后会详细描述。
  [<http://www.wwpdb.org/documentation/file-format-content/format33/sect7.html>]
* `CRYST1`: 标示晶胞参数、空间群和Z值。这部分可能对我们设置搜索空间有帮助。
  [<http://www.wwpdb.org/documentation/file-format-content/format33/sect8.html>]

```
DBREF  1HSG A    1    99  UNP    P03367   POL_HV1BR       69    167             
DBREF  1HSG B    1    99  UNP    P03367   POL_HV1BR       69    167             
SEQRES   1 A   99  PRO GLN ILE THR LEU TRP GLN ARG PRO LEU VAL THR ILE          
SEQRES   7 A   99  PRO THR PRO VAL ASN ILE ILE GLY ARG ASN LEU LEU THR          
SEQRES   8 A   99  GLN ILE GLY CYS THR LEU ASN PHE                              
SEQRES   1 B   99  PRO GLN ILE THR LEU TRP GLN ARG PRO LEU VAL THR ILE          
SEQRES   2 B   99  LYS ILE GLY GLY GLN LEU LYS GLU ALA LEU LEU ASP THR          
SEQRES   8 B   99  GLN ILE GLY CYS THR LEU ASN PHE                              
HET    MK1  B 902      45                                                       
HETNAM     MK1 N-[2(R)-HYDROXY-1(S)-INDANYL]-5-[(2(S)-TERTIARY                  
HETNAM   2 MK1  BUTYLAMINOCARBONYL)-4(3-PYRIDYLMETHYL)PIPERAZINO]-              
HETNAM   3 MK1  4(S)-HYDROXY-2(R)-PHENYLMETHYLPENTANAMIDE                       
HETSYN     MK1 INDINAVIR                                                        
FORMUL   3  MK1    C36 H47 N5 O4                                                
FORMUL   4  HOH   *127(H2 O)                                                    
HELIX    1   1 ARG A   87  LEU A   90  1                                   4    
HELIX    2   2 ARG B   87  LEU B   90  1                                   4    
SHEET    1   A 2 LEU A  10  ILE A  15  0                                        
SHEET    2   A 2 GLN A  18  LEU A  23 -1  N  ALA A  22   O  VAL A  11           
SHEET    1   B 4 VAL A  32  GLU A  34  0                                        
SITE     1 AC1 20 ARG A   8  ASP A  25  GLY A  27  GLY A  48                    
SITE     2 AC1 20 GLY A  49  VAL A  82  ARG B   8  ASP B  25                    
SITE     3 AC1 20 GLY B  27  ALA B  28  ASP B  29  ASP B  30                    
SITE     4 AC1 20 VAL B  32  GLY B  48  GLY B  49  ILE B  50                    
SITE     5 AC1 20 PRO B  81  HOH B 308  HOH B 313  HOH B 444                    
CRYST1   59.570   87.070   46.710  90.00  90.00  90.00 P 21 21 2     8          
ORIGX1      1.000000  0.000000  0.000000        0.00000                         
ORIGX2      0.000000  1.000000  0.000000        0.00000                         
ORIGX3      0.000000  0.000000  1.000000        0.00000                         
SCALE1      0.016787  0.000000  0.000000        0.00000                         
SCALE2      0.000000  0.011485  0.000000        0.00000                         
SCALE3      0.000000  0.000000  0.021409        0.00000                         
```

原子坐标

* `ATOM`: 标记氨基酸或核苷酸的坐标，依次包含原子的标号、原子名字
  (三个字符，若有第4个字符标示原子另外的构象)、残基名字、链、
  残基在序列的编号(4位数，若有第5位则为残基插入)、原子的坐标(x, y, z)、
  occupancy、温度、元素符号。【注：此简易描述只为简单理解PDB文件而写；
  若需用程序解析PDB文件，请参照官方文档来设计程序。】
* `TER`: 标记一条链的结束。 

```
ATOM      1  N   PRO A   1      29.361  39.686   5.862  1.00 38.10           N  
ATOM      2  CA  PRO A   1      30.307  38.663   5.319  1.00 40.62           C  
ATOM      3  C   PRO A   1      29.760  38.071   4.022  1.00 42.64           C  
ATOM      4  O   PRO A   1      28.600  38.302   3.676  1.00 43.40           O  
ATOM      5  CB  PRO A   1      30.508  37.541   6.342  1.00 37.87           C  
ATOM    757  CZ  PHE A  99      20.700  32.221  -9.700  1.00 27.25           C  
TER     758      PHE A  99                                                      
ATOM    759  N   PRO B   1      22.659  36.727 -10.823  1.00 48.12           N  
ATOM    760  CA  PRO B   1      21.708  37.741 -10.269  1.00 43.36           C  
ATOM   1513  CE1 PHE B  99      25.450  37.240   6.756  1.00 37.02           C  
ATOM   1514  CE2 PHE B  99      25.473  38.988   8.409  1.00 37.11           C  
ATOM   1515  CZ  PHE B  99      25.658  37.663   8.073  1.00 36.24           C  
TER    1516      PHE B  99                                                      
```

* `HETATM`: 测定了坐标的非聚合物或非标准分子部分，如水分子、
  结合的小分子化合物。

```
HETATM 1517  N1  MK1 B 902       9.280  23.763   3.004  1.00 28.25           N  
HETATM 1518  C1  MK1 B 902       9.498  23.983   4.459  1.00 30.30           C  
HETATM 1519  C2  MK1 B 902      10.591  24.905   4.962  1.00 27.27           C  
HETATM 1560  C35 MK1 B 902       4.654  23.774   4.136  1.00 49.34           C  
HETATM 1561  C36 MK1 B 902       5.905  23.211   3.897  1.00 44.71           C  
HETATM 1562  O   HOH A 305      20.857  43.192  21.450  1.00 63.07           O  
HETATM 1563  O   HOH A 307      14.076  19.789  19.440  1.00 63.34           O  
HETATM 1687  O   HOH B 613      24.127 -10.994  -0.982  1.00 64.49           O  
HETATM 1688  O   HOH B 617      30.112  17.912  -4.791  1.00 54.09           O  
```

* `CONECT`: 标示原子之间的连接，每一列为原子的编号。主要用于`HET`基团
  的连接。这些记录是自动生成的，也是强制性要有的。
* `MASTER`: 记录坐标的行数等信息
* `END`: 文件结尾

```
CONECT 1517 1518 1529 1555                                                      
CONECT 1518 1517 1519                                                           
CONECT 1519 1518 1520 1527                                                      
CONECT 1520 1519 1521 1522                                                      
CONECT 1561 1556 1560                                                           
MASTER      274    0    1    2   17    0    5    6 1686    2   45   16          
END                                                                             
```

PDBQT文件

PDBQT文件比PDB文件多两列，在原子坐标的后面增添了原子的局部电荷(partial
charges)和AutoDock可以识别原子类型代码。

在利用Vinna做Docking时，受体和配体都要获得PDBQT文件，一般包含下面两部
分信息：

  * 加斯泰格尔原子局部电荷
  * 联合原子模型展示（包括极性氢），首先对分子加氢然后计算其局部电荷。
    任何有氢键结合的非极性重原子的电荷需加上与其连接的氢的电荷，然后移
    除这些氢原子。
  * Gasteiger PEOE partial charges 
  * A united-atom representation (i.e. only polar hydrogens). A united
    atom representation can be obtained by first computing the partial
    charges for an all-hydrogen model of the molecule. Then,  for each
    non-polar heavy atom that has any hydrogens bonded to it,  the
    partial charge of the hydrogen should be added to that of the
    bonded heavy atom,  then this hydrogen atom can be deleted.)

```
REMARK   4 XXXX COMPLIES WITH FORMAT V. 2.0
ATOM      1  N   PRO A   1      29.361  39.686   5.862  1.00 38.10    -0.038 N 
ATOM      2  HN1 PRO A   1      28.682  40.038   5.187  1.00  0.00     0.280 HD
ATOM      3  HN2 PRO A   1      29.784  40.592   6.064  1.00  0.00     0.280 HD
ATOM      4  CA  PRO A   1      30.307  38.663   5.319  1.00 40.62     0.259 C 
ATOM      5  C   PRO A   1      29.760  38.071   4.022  1.00 42.64     0.259 C 
ATOM      6  O   PRO A   1      28.600  38.302   3.676  1.00 43.40    -0.271 OA
TER     923      PHE A  99 
ATOM    923  N   PRO B   1      22.659  36.727 -10.823  1.00 48.12    -0.038 N 
ATOM    924  HN1 PRO B   1      23.408  37.118 -11.394  1.00  0.00     0.280 HD
ATOM    925  HN2 PRO B   1      23.268  36.295 -10.128  1.00  0.00     0.280 HD
ATOM    926  CA  PRO B   1      21.708  37.741 -10.269  1.00 43.36     0.259 C 
ATOM   1844  CZ  PHE B  99      25.658  37.663   8.073  1.00 36.24     0.000 A 
TER    1845      PHE B  99 
```

AutoDock中配体可以为柔性结构，使用`torsion tree`来代表配体中固定的和可
选择的部分。在这个树中，有一个根，多个分支，其中分支可以嵌套。每一个分
支代表一个可以选择的键。在PDBQT文件中表示如下：
  
  * `ROOT`记录标记分子刚性部分的起始。
  * 刚性root包含一个或多个PDBQT-格式的`ATOM`或`HETATM`记录。
    这些记录与其在PDB文件中的含义类似, 只是在最后2列增加了电荷信息和
	原子类型信息。【注：这个文件的解析请见参考资料中的英文文档，此中文
	介绍只是为了方便理解】
  * `ENDROOT`记录标记配体刚性部分的结束。`ROOT/ENDROOT`原子块一般出现
    在PDBQT文件中的首部。如果我们想把配体的某部分作为刚性处理，则在其
	前后加上`ROOT/ENDROOT`标签即可。
  * 配体可选择部分包含于`BRANCH/ENDBRANCH`记录中间。
    `BRANCH`和`ENDBRANCH`记录行包含两个空格分开的数字，代表可旋转的键
	连接的第一个和第二个原子的编号。`BRANCH/ENDBRANCH`记录中间的记录旋转键中
	间的`ATOM/HETATM`记录。另外`BRANCH/ENDBRANCH`记录可以嵌套。
  * 配体PDBQT文件的最后一行为`TORSDOF`记录。这个记录包含一个整数，
    代表配体自由扭转度，这一值不依赖于可旋转的键的数目，而是取决于前述
	记录。【注:最后半句未理解，选择直译，请参照原文理解】

```
REMARK  14 active torsions:
REMARK  status: ('A' for Active; 'I' for Inactive)
REMARK    1  A    between atoms: N1_1517  and  C31_1559 
REMARK    2  A    between atoms: C2_1519  and  C3_1520 
REMARK       I    between atoms: C3_1520  and  N2_1522 
REMARK    4  A    between atoms: N3_1528  and  C10_1531 
REMARK   13  A    between atoms: C23_1549  and  O4_1550 
REMARK   14  A    between atoms: C31_1559  and  C32_1560 
ROOT
HETATM    1  N1  MK1 B 902       9.280  23.763   3.004  1.00 28.25     0.146 N 
HETATM    2  C1  MK1 B 902       9.498  23.983   4.459  1.00 30.30     0.282 C 
HETATM    6  C9  MK1 B 902      10.440  23.182   2.493  1.00 27.47     0.274 C 
ENDROOT
BRANCH   1   7
HETATM    7  C31 MK1 B 902       8.033  23.100   2.604  1.00 36.25     0.278 C 
BRANCH   7   8
HETATM    8  C32 MK1 B 902       6.666  23.739   2.876  1.00 42.75     0.028 A 
HETATM    9  C36 MK1 B 902       5.905  23.211   3.897  1.00 44.71     0.001 A 
HETATM   10  C35 MK1 B 902       4.654  23.774   4.136  1.00 49.34     0.018 A 
HETATM   11  C34 MK1 B 902       4.207  24.839   3.348  1.00 50.60     0.072 A 
HETATM   12  N5  MK1 B 902       4.911  25.430   2.300  1.00 51.38    -0.351 N 
HETATM   13  C33 MK1 B 902       6.158  24.808   2.124  1.00 47.41     0.070 A 
HETATM   14  H5  MK1 B 902       4.567  26.208   1.737  1.00  0.00     0.166 HD
ENDBRANCH   7   8
ENDBRANCH   1   7
TORSDOF 14
```



### 用到的文件列表

原始文件
	
  * [1hsg.pdb 蛋白小分子晶体结构]({{ site.img_url }}/docking/1hsg.pdb)
  * [1OHR.pdb 蛋白小分子晶体结构]({{ site.img_url }}/docking/1OHR.pdb)

处理后文件
  * [1hsg_prot.pdb 提取的蛋白结构]({{ site.img_url }}/docking/1hsg_prot.pdb)
  * [indinavir.pdb 提取的小分子结构]({{ site.img_url }}/docking/indinavir.pdb)
  * [1hsg_prot.pdbqt 转换后的蛋白结构]({{ site.img_url }}/docking/1hsg_prot.pdbqt)
  * [indinavir.pdbqt 转换后的小分子结构]({{ site.img_url }}/docking/indinavir.pdbqt)
  * [1hsg_indinavir_dockingResult.pdbqt 上面两个分子的docking结果]({{ site.img_url }}/docking/1hsg_indinavir_dockingResult.pdbqt)
  * [1hsg_prot_all_h.pdbqt 转换后的蛋白结构(加所有的氢)]({{ site.img_url }}/docking/1hsg_prot_all_h.pdbqt)
  * [1hsg_prot_all_h.pdbqt 转换后的小分子结构(加所有的氢)]({{ site.img_url }}/docking/1hsg_prot_all_h.pdbqt)
  * [1hsg_indinavir_dockingResultAllH.pdbqt 上面两个分子的docking结果]({{ site.img_url }}/docking/1hsg_indinavir_dockingResultAllH.pdbqt)
  * [1hsg_indinavir_original_tutorial_result.pdbqt 原始教程中docking结果]({{ site.img_url }}/docking/1hsg_indinavir_original_tutorial_result.pdbqt)
	
	


### 参考

* Detailed tutorial <http://sbcb.bioch.ox.ac.uk/users/greg/teaching/docking-2012.html>
* 官方文档 <http://vina.scripps.edu>
* PyMOL操作手册 <https://pymolwiki.org/index.php/Practical_Pymol_for_Beginners>
* PyMOL APBS <https://pymolwiki.org/index.php/APBS>
* PDBQT文件格式解释 <http://autodock.scripps.edu/faqs-help/faq/what-is-the-format-of-a-pdbqt-file>
* APBS使用文档<http://www.poissonboltzmann.org/examples/comp_tut/>



