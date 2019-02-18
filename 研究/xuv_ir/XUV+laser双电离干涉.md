# 干涉成因
  1.  从Lorentz meets fano这个文章的角度考虑，干涉可能是来源于激光场导致的"脉冲性"缀饰作用。相位为 $\phi_{laser} = \frac{-\Delta E\Delta t}{\hbar}$
  2.  从Attosecond dynamics through a Fano

  resonance这个文章的角度考虑，干涉可能是来源于激光场导致的末态连续态分布变化。单个XUV光子已经可以导致电离，激光对电离过程（概率）没有影响,干涉是两种末态之间的关联。这种类型的干涉有一些发生条件：两种通道概率幅比较近；激光场比较弱（不是相对XUV场）； 谐波阶次足够大。

# 微扰计算
  微扰计算可以揭示双光子双电离中的干涉信息，也可以指导TDSE计算的参数选取。

## 微扰方法
   双光子电离的概率幅可以用相应两个单光子电离过程来描述，Jiang2016的PRL里面讲到这种方法在非次序区同样成立。微扰法的电子能谱为：
   <!-- #+BEGIN_latex latex
   \begin{equation*} -->
   $$P(E_1, E_2) = 1/2(\frac{c}{4\pi^2})^2|\sqrt{\frac{\sigma^{He}(E_1)\sigma^{He^+}(E_2)}{\omega_{ai}\omega_{fa}}}K(E_a) + \sqrt{\frac{\sigma^{He}(E_{2})\sigma^{He^+}(E_1)}{\omega_{ai}\omega_{fa}}}K(E_b)|^2$$
   <!-- \end{equation*} -->
   <!-- #+END_latex    -->
   其中
   <!-- #+BEGIN_latex latex
   \begin{equation*} -->
$$K(E_a)=\int_{-\infty}^{\infty}\int_{-\infty}^{\tau_1}F(\tau_1)F(\tau_2)e^{i((Ea-Ei)*\tau_1+(Ef-Ea)*\tau_2)}d\tau_1d\tau_2$$
   <!-- \end{equation*}
   #+END_latex    -->
   在一维情形下，动量谱为
$$   P(k_1, k_2) = k_1k_2P(E_1,E_2)$$
### 数值微扰的问题
- Jiang的Double ionization of He by time-delayd attosecond pulses中的关联电子能谱可以重复出来，但Observing electron-correlation features in two-photon double ionization of helium的结果重复不正确,结果应该是3维和1维结果的差异
- 在我自己的2+1双电离情况下，动量谱计算结果受dt的影响很严重，相对精度eps只能设成1e-4，更低的压根计算不下去。另外，对于同一个脉冲，前后加上无场演化的部分之后，动量谱也不一样；在不同脉宽下面的结果也不一样。暂时不清楚这种问题是程序的bug还是对微扰法理解上面的不对。
- 结果证明，微扰法公式在数值上等效于一个二维Fourier变换，只是被积函数为$F(\tau_1)F(\tau_2)*(\tau_1>\tau_2)$.

## 微扰和TDSE
### 双脉冲
#### 长脉冲

   | w1   | w2   | w3  | $\tau$ | delay     |
   | ---- | ---- | --- | ------ | --------- |
   | 1.86 | 1.92 | 0.0 | 5 fs   | 1.5$\tau$ |

   只有双环，微扰的为下图,和TDSE结果一致

   ![微扰。长脉宽，无重叠。双环。](figs/perturbation/sit1.png)

   如果有重叠部分，则只有一个环，可以看作环没有分开。和TDSE结果一致。
   继续增加脉宽(10、30、40 fs)，发现双环变细(TDSE未算)，如果两个脉冲之间有重叠部分，则出现三环，和TDSE结果一致,只是TDSE结果在此脉宽下三环仍分不开。

   Table 1: (1)微扰。长脉宽，无重叠。双环 (2)微扰。长脉宽，有重叠。三环 

   ![微扰。长脉宽，无重叠。双环](figs/perturbation/sit4.png) ![微扰。长脉宽，有重叠。三环](figs/perturbation/sit5.png)

#### 短脉冲

   | w1   | w2   | w3  | \tau   | delay |
   | ---- | ---- | --- | ------ | ----- |
   | 1.86 | 1.92 | 0.0 | 0.5 fs | 4\tau |

   delay=4$\tau$; 时，分裂成许多小环; delay = 0时，环不分裂.交换w1、w2没有影响。这个结果和PRL 103, 253001 (2009)一致。但是此文章中的w1、w2相差一倍。

   Table 2: (1)微扰。短脉宽，delay=4$\tau$;  (2)微扰。短脉宽，delay=0

   ![微扰。短脉宽，delay=4$\tau$](figs/perturbation/sit2.png)
   ![微扰。短脉宽，delay=0](figs/perturbation/sit3.png)

#### 非共振
   | w1  | w2  | w3  | $\tau$ | delay  |
   | --- | --- | --- | ------ | ------ |
   | 2.5 | 2.7 | 0.1 | 20 fs  | $\tau$ |



   TDSE中有干涉，

   ![img](figs/perturbation/non-re.png "TDSE.非共振。长脉宽")

   | w1  | w2  | w3   | $\tau$ | delay  |
   | --- | --- | ---- | ------ | ------ |
   | 3.1 | 3.2 | 0.05 | 10 fs  | $\tau$ |


   这种情况下的微扰计算对应于xuv单光子双电离+红外调制的结果,实际上可能更明显的单光子双电离过程反而得不到。结果为:

   ![微扰.非共振。XUV+IR](figs/perturbation/2.1-2.2-10fs.png)

   其中三个大环分别对应 (其中的第二大环的分裂随着delay增加而增多。)

   1.  w1-w3
   2.  w1+w3=w2-w3
   3.  w2+w3

      
# TDSE计算

##  XUV+IR
   | w1   | w2   | I1   | I2      | $\tau$ | delay |
   | ---- | ---- | ---- | ------- | ------ | ----- |
   | 1.86 | 0.03 | 1e15 | I1/1000 | 16fs   | 0     |
   !["XUV+IR"](figs/tdse-xuv+laser/1.png)
    
## 中等(5fs)脉冲 2XUV+IR I1 = I2
   | w1   | w2   | w3   | I1   | I2      | \tau | delay    |
   | ---- | ---- | ---- | ---- | ------- | ---- | -------- |
   | 1.86 | 1.92 | 0.03 | 1e14 | I1/1000 | 5fs  | 0        |
   | 1.86 | 1.92 | 0.03 | 1e14 | I1/1000 | 5fs  | 0.25\tau |
   | 1.86 | 1.92 | 0.03 | 1e14 | I1/1000 | 5fs  | 1.5\tau  |
   | 1.86 | 1.92 | 0.03 | 1e14 | I1/1000 | 10fs | 0        |
   Table 3: (1)TDSE。5fs，delay=0 (2)TDSE。5fs，delay=0.25 $\tau$; (3)TDSE。5fs，delay=1.5$\tau$
   ![TDSE。5fs，delay=0](figs/tdse-xuv+laser/0.png)
   ![TDSE。5fs，delay=0.25](figs/tdse-xuv+laser/0.25.png)
   ![TDSE。5fs，delay=1.5$\tau$](figs/tdse-xuv+laser/1.5.png)
   ![TDSE。10fs，delay=0](figs/tdse-xuv+laser/eq-0.png)

### 包含文件夹

  1.  !!delay-0.5
  2.  !!delay-1
  3.  !!delay-1.5
  4.  !!delay-2.0
  5.  !!delay-2.5
  6.  !!delay-3
  7.  !!delay-3-10fs


### 解释

  通过相应情况下的微扰计算和长波长时候的计算可以推测没有红外时候的结果。结果是，对于5fs的情况而言，delay=0j时没有分裂，delay=0.25时，有三重分裂，dealy=1.5时，有两重分裂，且这些分裂都是均匀的，说明这里的激光场的作用可能是ac-stark效应，只不过这种ac-stark效应是动态的，这里的延迟不是XUV之间的，而是XUV相对于激光场的。不同部分产生的ac-stark效应方向相反。对于delay=1.5的时候而言，有些部分ac-stark效应使环接近，有些部分使环分开。问题是，这个Stark效应是怎么分布的呢？


    
## 光强低、双倍差、零延迟
   | w1   | w2   | w3   | I1   | I2      | \tau | delay |
   | ---- | ---- | ---- | ---- | ------- | ---- | ----- |
   | 1.86 | 1.92 | 0.06 | 1e14 | I1/1000 | 5fs  | 0     |
   | 1.56 | 1.66 | 0.1  | 1e14 | I1/1000 | 15fs | 0     |

### 包含文件夹
  1.  !!0-30
  2.  !!0-30-longer
  3.  !!1.56-longer
   
  结果，8fs时，两个方向都没有干涉；14fs时，成细的三环, 非共振时候也一样


## 光强低、双倍差有延迟
   1.  !!2.0-1.56-longer
   2.  !!2.0
   3.  !!1.0
   4.  !!3.0
   5.  !!4.0
   6.  !!4.0-longer


## 两个脉冲、无延迟
### 包含文件夹
  1. two-4e-14
  2. two-4e-15

## 两个脉冲、有延迟

   没有角方向干涉,按照微扰的分析，应该是脉宽太长,基本上1fs都算太长了，同时delay太小了。

   1.  !!1.74-1.86-30-two
   2.  !!1.86-1.92-1fs-0-two
   3.  !!1.86-1.92-5fs-1.5
   4.  1.86-1.92-2fs-0-two


## 共振

   $\Delta$ w 太大时没有明显分裂

    
### 包含文件夹

  1.  1.86-1.92-4fs-0
  2.  1.86-1.92-10fs-0
  3.  1.86-1.92-40fs-0
  4.  w1.86-w1.70-w0.08-i1e15-r2-r15-t0
  5.  w1.86-w1.74-w0.06-i1e15-r2-r15-t0


## 非共振、无延迟无干涉

   | w1   | w2   | w3   | I1   | I2   | \tau    | delay |
   | ---- | ---- | ---- | ---- | ---- | ------- | ----- |
   | 1.50 | 1.56 | 0.03 | 1e15 | I1/2 | I1/1000 | 25fs  | 0 |
   | 1.60 | 1.66 | 0.03 | 1e15 | I1/2 | I1/1000 | 25fs  |   |


    
### 包含文件夹

  1.  1.50-1.56
  2.  1.60-1.66

  无角向干涉，可能是脉宽25fs太大了,也可能是由于通道w1 w2强度不一致。5fs又太小了，干涉没分开。


    
## 非共振、无延迟有干涉

   | w1   | w2   | w3   | I1   | I2  | \tau    | delay |
   | ---- | ---- | ---- | ---- | --- | ------- | ----- |
   | 2.5  | 2.7  | 0.1  | 1e15 | I1  | I1/1000 | 20fs  |
   | 1.60 | 1.66 | 0.03 | 1e15 | I1  | I1/1000 | 5fs   |
   | 1.70 | 1.76 | 0.03 | 1e15 | I1  | I1/1000 | 20fs  |


   边上有角向干涉，中间没有，有点类似Feist PRL的结果。

   ![](figs/tdse-xuv+laser/2.5-2.7.png)
   ![](figs/tdse-xuv+laser/1.6-1.66.png)

    
### 包含文件夹

  1.  1.60-1.66-5fs-0
  2.  1.70-1.76-0.03-1e15-0-long
  3.  1.70-1.76-0.03-1e15-1.5
  4.  1.70-1.76-0.03-1e15-d0-50


## 非共振、单光子无延迟

   | w1  | w2  | w3   | I1   | I2  | \tau    | delay |
   | --- | --- | ---- | ---- | --- | ------- | ----- |
   | 3.2 | 3.3 | 0.05 | 1e15 | I1  | I1/1000 | 20fs  |
   | 3.2 | 3.3 | 0.05 | 1e15 | I1  | I1/400  | 20fs  |


   Table 4:  TDSE, 3.2+3.3, 20fs

   ![](figs/tdse-xuv+laser/single.png)
   ![](figs/tdse-xuv+laser/single20.png)

## 有意思的结果

   1.  delay-3
   2.  delay-0-10fs
   3.  delay-3-10fs
   4.  delay-5.0
   5.  1.56-longer
   6.  delay-0.5
   7.  delay-1
   8.  single-photon
   9.  1.62-1.70
   10. w1.86-w1.92-w0.03-i1e15-r2-r30-t0/