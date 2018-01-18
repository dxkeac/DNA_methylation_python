# python_find_dmr


- 这些脚本是用来求拟南芥野生型和突变体差异甲基化区域的。



- 使用这些脚本需要知道：

程序都需要python3环境，程序需要安装biopyton,可以用pip或者conda来安装。

（拟南芥5条染色体fa文件、2个表型甲基化位点文件都在testdata存放）




- 总的流程是：

第一步：使用biopython从fa文件得出各条染色体长度；


第二步：将总的基因组分成间隔相等的bin；


第三步：将两个表型的bismark软件coverage2cytosine命令生成的文件合并；


第四步：用第三步合并的文件和第二步生成的bin文件求差异甲基化区域。




	
	python3 Calchrlength_v.py Chr1 Chr2 Chr3 Chr4 Chr5 TAIR10_chr1.fa TAIR10_chr2.fa TAIR10_chr3.fa TAIR10_chr4.fa TAIR10_chr5.fa arabid_chr_length.txt

	python3 ChrBin_v.py --chrlenfile arabid_chr_length.txt  --bin 1000 --step 500 -o arabin.txt

	python3 CombineBisGenome_v.py --fn1 col0_Chr1_1000row_genome --fn2 linc3-7_Chr1_1000row_genome -o col0_lin3-7_Chr1.txt

    python3 ChrBinFindDmr_v.py --fn1 col0_lin3-7_Chr1.txt --fn2 arabin.txt --Ctype CG --depth 4 --mCnum 5 --diff 0.3 --pval 0.01 -o col0_linc3-7_Chr1_CG_DMR




- 1.python3 Calchrlength_v.py



输入文件格式：

![](https://i.imgur.com/HO56I6j.jpg)




 输出文件格式：

![](https://i.imgur.com/feItr5V.jpg)




- 2.python3 ChrBin_v.py -h

![](https://i.imgur.com/LKbDEJm.jpg)



输入文件格式：

![](https://i.imgur.com/84N7u1K.jpg)



输出文件格式：

![](https://i.imgur.com/wXIdECC.jpg)




- 3.python3 CombineBisGenome_v.py -h

![](https://i.imgur.com/8bLVqxL.jpg)



输入文件格式：（另一个格式相同）

![](https://i.imgur.com/YF4FqRm.jpg)




 输出文件格式：

![](https://i.imgur.com/5RDIRx7.jpg)

- 
- 


- 4.python3 ChrBinFindDmr_v.py -h



输入文件格式如下：

![](https://i.imgur.com/zquSztw.jpg)

![](https://i.imgur.com/d9Tgemw.jpg)



输出文件格式如下：


染色体		起始区间		结束区间		1甲基化水平		2甲基化水平		甲基化水平差值	P值		

![](https://i.imgur.com/K5oVBzp.jpg)


