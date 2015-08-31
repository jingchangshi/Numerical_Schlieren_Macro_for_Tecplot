# Numerical Schlieren Macro for Tecplot

## 说明

+ 用于`Tecplot`软件中绘制流场的数值纹影图，与激波相关。
+ 此代码基于下一部分内容`Note on Numerical Schlieren`

## 代码

+ 包含`2`个文件
  - `NumericalSchlieren-1.mcr`用于计算$\nabla \rho$
  - `NumericalSchlieren-2.mcr`用于计算最终纹影数值
  - `{Constant}`数值根据需要改变
  - 最后计算`{Sch}`的公式中指数`5`根据需要改变
+ 见[GitHub](https://github.com/desperadoshi/Numerical_Schlieren_Macro_for_Tecplot)

## Note on Numerical Schlieren

The flow images resulting from experiment are usually schlieren pictures giving patterns integrated along the spanwise direction. To compare our numerical flow fields with experimental ones, we usually calculate an averaged density gradient field as

$$
\bar{\nabla \rho} (x, y) = \frac{1}{L_{z}} \int | \nabla \rho (x, y, z) | dz
$$

Then it is visualized using the "numerical schlieren" technique put forward by [1] (as a half-tone grey-scale picture with a special nonlinear scale).

In the particular case of visualization of the flow field in the problem of RR/blast wave interaction the pictures given in my short note were not integrated along transverse coordinate. These are just $\nabla \rho (x, y, z = 0)$. I think the integrated numerical schlieren are somewhat smeared probably because of low resolution used in my preliminary computations.

So, the procedure is as follows. First, we compute the density gradient in plane $z = const$:

$$
| \nabla \rho (x, y) | = \sqrt{(\frac{\partial \rho}{\partial x})^{2} + (\frac{\partial \rho}{\partial y})^{2}}
$$

We may then average it along $z$ axis if we want.

Next, we determine a special non-linear scale for the above (see [1]). I use the following function.

$$
\begin{aligned}
Sch(x, y) &= exp( - c_{k} S(x, y) ) \\
S(x, y) &= \frac{|\nabla \rho (x, y)| - |\nabla \rho (x, y)|_{0}}{|\nabla \rho (x, y)|_{1} - |\nabla \rho (x, y)|_{0}} \\
\end{aligned}
$$

Here $|\nabla \rho (x, y)|_{0} = c_{0} |\nabla \rho (x, y)|_{max_{x, y}}, |\nabla \rho (x, y)|_{1} = c_{1} |\nabla \rho (x, y)|_{max_{x, y}}$, and the constants are chosen as $c_{0} = -0.001, c_{1} = 0.05, c_{k} = 5$.

This function is then plotted in greyscale.

+ Reference

    [1] Quirk JJ (1994) A contribution to the great Riemann solver debate. Int J Number Methods in Fluids 18: 555-574.

