---
source: sources/wiki-Gradient_descent.md
source_url: https://en.wikipedia.org/wiki/Gradient_descent
chunk: 2/4
---

## Solution of a linear system

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Steepest_descent.png/250px-Steepest_descent.png)](./File:Steepest_descent.png)The steepest descent algorithm applied to the [Wiener filter](./Wiener_filter)[[12]](./Gradient_descent#cite_note-12) 

Gradient descent can be used to solve a [system of linear equations](./System_of_linear_equations)

      A   x  − −   b  = 0   {\displaystyle \mathbf {A} \mathbf {x} -\mathbf {b} =0}  ![{\displaystyle \mathbf {A} \mathbf {x} -\mathbf {b} =0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/435e223a0da553ca83961b0af747b0a3567bfe26) 

reformulated as a quadratic minimization problem.
If the system matrix      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) is real [symmetric](./Symmetric_matrix) and [positive-definite](./Positive-definite_matrix), an objective function is defined as the quadratic function, with minimization of

     f (  x  ) =   x   ⊤ ⊤     A   x  − −  2   x   ⊤ ⊤     b  ,   {\displaystyle f(\mathbf {x} )=\mathbf {x} ^{\top }\mathbf {A} \mathbf {x} -2\mathbf {x} ^{\top }\mathbf {b} ,}  ![{\displaystyle f(\mathbf {x} )=\mathbf {x} ^{\top }\mathbf {A} \mathbf {x} -2\mathbf {x} ^{\top }\mathbf {b} ,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba4556b22259b1326230d6e75cb40fda87073029) 

so that

     ∇ ∇  f (  x  ) = 2 (  A   x  − −   b  ) .   {\displaystyle \nabla f(\mathbf {x} )=2(\mathbf {A} \mathbf {x} -\mathbf {b} ).}  ![{\displaystyle \nabla f(\mathbf {x} )=2(\mathbf {A} \mathbf {x} -\mathbf {b} ).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/769dc711ac488ef07e64a0ddc3fe4f0c35617ca3) 

For a general real matrix      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1), [linear least squares](./Linear_least_squares) define

     f (  x  ) =   ‖   A   x  − −   b   ‖   2   .   {\displaystyle f(\mathbf {x} )=\left\|\mathbf {A} \mathbf {x} -\mathbf {b} \right\|^{2}.}  ![{\displaystyle f(\mathbf {x} )=\left\|\mathbf {A} \mathbf {x} -\mathbf {b} \right\|^{2}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8e1c13e49915329e1a406839842e788ad4f21a7f) 

In traditional linear least squares for real      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) and      b    {\displaystyle \mathbf {b} }  ![{\displaystyle \mathbf {b} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/13ebf4628a1adf07133a6009e4a78bdd990c6eb9) the [Euclidean norm](./Euclidean_norm) is used, in which case

     ∇ ∇  f (  x  ) = 2   A   ⊤ ⊤    (  A   x  − −   b  ) .   {\displaystyle \nabla f(\mathbf {x} )=2\mathbf {A} ^{\top }(\mathbf {A} \mathbf {x} -\mathbf {b} ).}  ![{\displaystyle \nabla f(\mathbf {x} )=2\mathbf {A} ^{\top }(\mathbf {A} \mathbf {x} -\mathbf {b} ).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e65e5b1a7819a9b8449f15b7f031f83a4ac9f190) 

The [line search](./Line_search) minimization, finding the locally optimal step size     η η    {\displaystyle \eta }  ![{\displaystyle \eta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e4d701857cf5fbec133eebaf94deadf722537f64) on every iteration, can be performed analytically for quadratic functions, and explicit formulas for the locally optimal     η η    {\displaystyle \eta }  ![{\displaystyle \eta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e4d701857cf5fbec133eebaf94deadf722537f64) are known.[[6]](./Gradient_descent#cite_note-BP-6)[[13]](./Gradient_descent#cite_note-saad1996iterative-13)

 

For example, for real [symmetric](./Symmetric_matrix) and [positive-definite](./Positive-definite_matrix) matrix      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1), a simple algorithm can be as follows,[[6]](./Gradient_descent#cite_note-BP-6)

           repeat in the loop:         r  :=  b  − −   A x        η η  :=    r   ⊤ ⊤     r    /     r   ⊤ ⊤     A r          x  :=  x  + η η   r          if      r   ⊤ ⊤     r    is sufficiently small, then exit loop        end repeat loop        return    x    as the result        {\displaystyle {\begin{aligned}&{\text{repeat in the loop:}}\\&\qquad \mathbf {r} :=\mathbf {b} -\mathbf {Ax} \\&\qquad \eta :={\mathbf {r} ^{\top }\mathbf {r} }/{\mathbf {r} ^{\top }\mathbf {Ar} }\\&\qquad \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} \\&\qquad {\hbox{if }}\mathbf {r} ^{\top }\mathbf {r} {\text{ is sufficiently small, then exit loop}}\\&{\text{end repeat loop}}\\&{\text{return }}\mathbf {x} {\text{ as the result}}\end{aligned}}}  ![{\displaystyle {\begin{aligned}&{\text{repeat in the loop:}}\\&\qquad \mathbf {r} :=\mathbf {b} -\mathbf {Ax} \\&\qquad \eta :={\mathbf {r} ^{\top }\mathbf {r} }/{\mathbf {r} ^{\top }\mathbf {Ar} }\\&\qquad \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} \\&\qquad {\hbox{if }}\mathbf {r} ^{\top }\mathbf {r} {\text{ is sufficiently small, then exit loop}}\\&{\text{end repeat loop}}\\&{\text{return }}\mathbf {x} {\text{ as the result}}\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45b2d98ecf8d9c7a974384ca0e5364e45c23277a) 

To avoid multiplying by      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) twice per iteration,
we note that      x  :=  x  + η η   r    {\displaystyle \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} }  ![{\displaystyle \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/eec57220e5a6166f62d330bf03b967187dd9601e) implies      r  :=  r  − −  η η   A r    {\displaystyle \mathbf {r} :=\mathbf {r} -\eta \mathbf {Ar} }  ![{\displaystyle \mathbf {r} :=\mathbf {r} -\eta \mathbf {Ar} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/596f784bd1c487b5c58e8fc7d49da3f1803cc2b7), which gives the traditional algorithm,[[14]](./Gradient_descent#cite_note-:0-14)

           r  :=  b  − −   A x        repeat in the loop:        η η  :=    r   ⊤ ⊤     r    /     r   ⊤ ⊤     A r          x  :=  x  + η η   r          if      r   ⊤ ⊤     r    is sufficiently small, then exit loop         r  :=  r  − −  η η   A r        end repeat loop        return    x    as the result        {\displaystyle {\begin{aligned}&\mathbf {r} :=\mathbf {b} -\mathbf {Ax} \\&{\text{repeat in the loop:}}\\&\qquad \eta :={\mathbf {r} ^{\top }\mathbf {r} }/{\mathbf {r} ^{\top }\mathbf {Ar} }\\&\qquad \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} \\&\qquad {\hbox{if }}\mathbf {r} ^{\top }\mathbf {r} {\text{ is sufficiently small, then exit loop}}\\&\qquad \mathbf {r} :=\mathbf {r} -\eta \mathbf {Ar} \\&{\text{end repeat loop}}\\&{\text{return }}\mathbf {x} {\text{ as the result}}\end{aligned}}}  ![{\displaystyle {\begin{aligned}&\mathbf {r} :=\mathbf {b} -\mathbf {Ax} \\&{\text{repeat in the loop:}}\\&\qquad \eta :={\mathbf {r} ^{\top }\mathbf {r} }/{\mathbf {r} ^{\top }\mathbf {Ar} }\\&\qquad \mathbf {x} :=\mathbf {x} +\eta \mathbf {r} \\&\qquad {\hbox{if }}\mathbf {r} ^{\top }\mathbf {r} {\text{ is sufficiently small, then exit loop}}\\&\qquad \mathbf {r} :=\mathbf {r} -\eta \mathbf {Ar} \\&{\text{end repeat loop}}\\&{\text{return }}\mathbf {x} {\text{ as the result}}\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1fff635ae5452ba52667f206b2173ecca3660291)[![](//upload.wikimedia.org/wikipedia/commons/thumb/6/6c/Steepest_descent_convergence_path_for_A_%3D_2_2%2C_2_3.png/250px-Steepest_descent_convergence_path_for_A_%3D_2_2%2C_2_3.png)](./File:Steepest_descent_convergence_path_for_A_=_2_2,_2_3.png)Convergence path of steepest descent method for A = [[2, 2], [2, 3]] 

The method is rarely used for solving linear equations, with the [conjugate gradient method](./Conjugate_gradient_method) being one of the most popular alternatives. The number of gradient descent iterations is commonly proportional to the spectral [condition number](./Condition_number)     κ κ  (  A  )   {\displaystyle \kappa (\mathbf {A} )}  ![{\displaystyle \kappa (\mathbf {A} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f4a3dab1be502165a1ac693234b92db1c5ad660f) of the system matrix      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) (the ratio of the maximum to minimum [eigenvalues](./Eigenvalues) of       A   ⊤ ⊤     A    {\displaystyle \mathbf {A} ^{\top }\mathbf {A} }  ![{\displaystyle \mathbf {A} ^{\top }\mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/8fda2f40a3140773a86e8409b54d9ea7aa148f9e)), while the convergence of [conjugate gradient method](./Conjugate_gradient_method) is typically determined by a square root of the condition number, i.e., is much faster. Both methods can benefit from [preconditioning](./Preconditioner), where gradient descent may require less assumptions on the preconditioner.[[14]](./Gradient_descent#cite_note-:0-14)

 

### Geometric behavior and residual orthogonality

 

In steepest descent applied to solving      A x  =  b    {\displaystyle \mathbf {Ax} =\mathbf {b} }  ![{\displaystyle \mathbf {Ax} =\mathbf {b} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e68388b7df59f536a3bef4e70def2f2bb36f48c0), where      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) is symmetric positive-definite, the residual vectors       r   k   =  b  − −   A    x   k     {\displaystyle \mathbf {r} _{k}=\mathbf {b} -\mathbf {A} \mathbf {x} _{k}}  ![{\displaystyle \mathbf {r} _{k}=\mathbf {b} -\mathbf {A} \mathbf {x} _{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb35c202ad0912a4bb19012c7af3529163586b97) are orthogonal across iterations:

     ⟨ ⟨    r   k + 1   ,   r   k   ⟩ ⟩  = 0.   {\displaystyle \langle \mathbf {r} _{k+1},\mathbf {r} _{k}\rangle =0.}  ![{\displaystyle \langle \mathbf {r} _{k+1},\mathbf {r} _{k}\rangle =0.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/75f9a3bb5c53033de95a00b1c183b9de5f77345b) 

Because each step is taken in the steepest direction, steepest-descent steps alternate between directions aligned with the extreme axes of the elongated level sets.  When     κ κ  (  A  )   {\displaystyle \kappa (\mathbf {A} )}  ![{\displaystyle \kappa (\mathbf {A} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f4a3dab1be502165a1ac693234b92db1c5ad660f) is large, this produces a characteristic zig–zag path. The poor conditioning of      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1) is the primary cause of the slow convergence, and orthogonality of successive residuals reinforces this alternation.

 

As shown in the image on the right, steepest descent converges slowly due to the high condition number of      A    {\displaystyle \mathbf {A} }  ![{\displaystyle \mathbf {A} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0795cc96c75d81520a120482662b90f024c9a1a1), and the orthogonality of residuals forces each new direction to undo the overshoot from the previous step. The result is a path that zigzags toward the solution. This inefficiency is one reason conjugate gradient or preconditioning methods are preferred.[[15]](./Gradient_descent#cite_note-15)

 

## Solution of a non-linear system

 

Gradient descent can also be used to solve a system of [nonlinear equations](./Nonlinear_equation). Below is an example that shows how to use the gradient descent to solve for three unknown variables, *x*1, *x*2, and *x*3. This example shows one iteration of the gradient descent.

 

Consider the nonlinear system of equations

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/b5/Gradient_Descent_Example_Nonlinear_Equations.gif/500px-Gradient_Descent_Example_Nonlinear_Equations.gif)](./File:Gradient_Descent_Example_Nonlinear_Equations.gif)An animation showing the first 83 iterations of gradient descent applied to this example. Surfaces are [isosurfaces](./Isosurface) of     f (   x   ( n )   )   {\displaystyle f(\mathbf {x} ^{(n)})}  ![{\displaystyle f(\mathbf {x} ^{(n)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fddab40001c0d518f35ca0208a4d4abd282faa84) at current guess       x   ( n )     {\displaystyle \mathbf {x} ^{(n)}}  ![{\displaystyle \mathbf {x} ^{(n)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f499a0c7f0c98f9393b40fd64dd97b26f345c547), and arrows show the direction of descent. Due to a small and constant step size, the convergence is slow.      {    3  x  1   − −  cos ⁡ ⁡  (  x  2    x  3   ) − −     3 2    = 0     4  x  1   2   − −  625  x  2   2   + 2  x  2   − −  1 = 0     exp ⁡ ⁡  ( − −   x  1    x  2   ) + 20  x  3   +     10 π π  − −  3  3    = 0         {\displaystyle {\begin{cases}3x_{1}-\cos(x_{2}x_{3})-{\tfrac {3}{2}}=0\\4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1=0\\\exp(-x_{1}x_{2})+20x_{3}+{\tfrac {10\pi -3}{3}}=0\end{cases}}}  ![{\displaystyle {\begin{cases}3x_{1}-\cos(x_{2}x_{3})-{\tfrac {3}{2}}=0\\4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1=0\\\exp(-x_{1}x_{2})+20x_{3}+{\tfrac {10\pi -3}{3}}=0\end{cases}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/540a1ea603de51e040c6fe8034ce8ccb10b3f4d7) 

Let us introduce the associated function

     G (  x  ) =   [    3  x  1   − −  cos ⁡ ⁡  (  x  2    x  3   ) − −     3 2        4  x  1   2   − −  625  x  2   2   + 2  x  2   − −  1     exp ⁡ ⁡  ( − −   x  1    x  2   ) + 20  x  3   +     10 π π  − −  3  3       ]   ,   {\displaystyle G(\mathbf {x} )={\begin{bmatrix}3x_{1}-\cos(x_{2}x_{3})-{\tfrac {3}{2}}\\4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1\\\exp(-x_{1}x_{2})+20x_{3}+{\tfrac {10\pi -3}{3}}\\\end{bmatrix}},}  ![{\displaystyle G(\mathbf {x} )={\begin{bmatrix}3x_{1}-\cos(x_{2}x_{3})-{\tfrac {3}{2}}\\4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1\\\exp(-x_{1}x_{2})+20x_{3}+{\tfrac {10\pi -3}{3}}\\\end{bmatrix}},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b649372ae6174f11549dd035f107eac303b5377) 

where

      x  =   [     x  1        x  2        x  3      ]   .   {\displaystyle \mathbf {x} ={\begin{bmatrix}x_{1}\\x_{2}\\x_{3}\\\end{bmatrix}}.}  ![{\displaystyle \mathbf {x} ={\begin{bmatrix}x_{1}\\x_{2}\\x_{3}\\\end{bmatrix}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/669781ad6ed5e35cc494e28efac793c74311195f) 

One might now define the objective function

         f (  x  )    =   1 2    G  ⊤ ⊤    (  x  ) G (  x  )       =   1 2    [    (  3  x  1   − −  cos ⁡ ⁡  (  x  2    x  3   ) − −    3 2    )   2   +   (  4  x  1   2   − −  625  x  2   2   + 2  x  2   − −  1  )   2   +                (  exp ⁡ ⁡  ( − −   x  1    x  2   ) + 20  x  3   +    10 π π  − −  3  3    )   2   ]  ,       {\displaystyle {\begin{aligned}f(\mathbf {x} )&={\frac {1}{2}}G^{\top }(\mathbf {x} )G(\mathbf {x} )\\&={\frac {1}{2}}\left[\left(3x_{1}-\cos(x_{2}x_{3})-{\frac {3}{2}}\right)^{2}+\left(4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1\right)^{2}+\right.\\&{}\qquad \left.\left(\exp(-x_{1}x_{2})+20x_{3}+{\frac {10\pi -3}{3}}\right)^{2}\right],\end{aligned}}}  ![{\displaystyle {\begin{aligned}f(\mathbf {x} )&={\frac {1}{2}}G^{\top }(\mathbf {x} )G(\mathbf {x} )\\&={\frac {1}{2}}\left[\left(3x_{1}-\cos(x_{2}x_{3})-{\frac {3}{2}}\right)^{2}+\left(4x_{1}^{2}-625x_{2}^{2}+2x_{2}-1\right)^{2}+\right.\\&{}\qquad \left.\left(\exp(-x_{1}x_{2})+20x_{3}+{\frac {10\pi -3}{3}}\right)^{2}\right],\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/205d7f08ca51e53e3b010ca85c55de40d4c068be) 

which we will attempt to minimize. As an initial guess, let us use

       x   ( 0 )   =  0  =   [    0     0     0    ]   .   {\displaystyle \mathbf {x} ^{(0)}=\mathbf {0} ={\begin{bmatrix}0\\0\\0\\\end{bmatrix}}.}  ![{\displaystyle \mathbf {x} ^{(0)}=\mathbf {0} ={\begin{bmatrix}0\\0\\0\\\end{bmatrix}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/828f564078b2a3d2307d9a0388a0cc76f21716c4) 

We know that

       x   ( 1 )   =  0  − −   η η   0   ∇ ∇  f (  0  ) =  0  − −   η η   0    J  G   (  0   )  ⊤ ⊤    G (  0  ) ,   {\displaystyle \mathbf {x} ^{(1)}=\mathbf {0} -\eta _{0}\nabla f(\mathbf {0} )=\mathbf {0} -\eta _{0}J_{G}(\mathbf {0} )^{\top }G(\mathbf {0} ),}  ![{\displaystyle \mathbf {x} ^{(1)}=\mathbf {0} -\eta _{0}\nabla f(\mathbf {0} )=\mathbf {0} -\eta _{0}J_{G}(\mathbf {0} )^{\top }G(\mathbf {0} ),}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01a8568ba794f4fd29ffc61bd210ebfed8ecabf5) 

where the [Jacobian matrix](./Jacobian_matrix)      J  G     {\displaystyle J_{G}}  ![{\displaystyle J_{G}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eb18051dfc2735d7015023e0d0615ad6cb52af77) is given by

      J  G   (  x  ) =   [    3   sin ⁡ ⁡  (  x  2    x  3   )  x  3     sin ⁡ ⁡  (  x  2    x  3   )  x  2       8  x  1     − −  1250  x  2   + 2   0     − −   x  2   exp ⁡ ⁡   ( − −   x  1    x  2   )    − −   x  1   exp ⁡ ⁡  ( − −   x  1    x  2   )   20    ]   .   {\displaystyle J_{G}(\mathbf {x} )={\begin{bmatrix}3&\sin(x_{2}x_{3})x_{3}&\sin(x_{2}x_{3})x_{2}\\8x_{1}&-1250x_{2}+2&0\\-x_{2}\exp {(-x_{1}x_{2})}&-x_{1}\exp(-x_{1}x_{2})&20\\\end{bmatrix}}.}  ![{\displaystyle J_{G}(\mathbf {x} )={\begin{bmatrix}3&\sin(x_{2}x_{3})x_{3}&\sin(x_{2}x_{3})x_{2}\\8x_{1}&-1250x_{2}+2&0\\-x_{2}\exp {(-x_{1}x_{2})}&-x_{1}\exp(-x_{1}x_{2})&20\\\end{bmatrix}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2bac1f9f28f50a955bea2944d1ca3d5f3918c340) 

We calculate:

      J  G   (  0  ) =   [    3   0   0     0   2   0     0   0   20    ]   ,  G (  0  ) =   [    − −  2.5     − −  1     10.472    ]   .   {\displaystyle J_{G}(\mathbf {0} )={\begin{bmatrix}3&0&0\\0&2&0\\0&0&20\end{bmatrix}},\qquad G(\mathbf {0} )={\begin{bmatrix}-2.5\\-1\\10.472\end{bmatrix}}.}  ![{\displaystyle J_{G}(\mathbf {0} )={\begin{bmatrix}3&0&0\\0&2&0\\0&0&20\end{bmatrix}},\qquad G(\mathbf {0} )={\begin{bmatrix}-2.5\\-1\\10.472\end{bmatrix}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e90a90b31c95af2cccea00cf025c041e5228c647) 

Thus

       x   ( 1 )   =  0  − −   η η   0     [    − −  7.5     − −  2     209.44    ]   ,   {\displaystyle \mathbf {x} ^{(1)}=\mathbf {0} -\eta _{0}{\begin{bmatrix}-7.5\\-2\\209.44\end{bmatrix}},}  ![{\displaystyle \mathbf {x} ^{(1)}=\mathbf {0} -\eta _{0}{\begin{bmatrix}-7.5\\-2\\209.44\end{bmatrix}},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/11c69f5345d6222e6238b4ae22bc3eb1ca0c0924) 

and

     f (  0  ) = 0.5  (  ( − −  2.5  )  2   + ( − −  1  )  2   + ( 10.472  )  2    )  = 58.456.   {\displaystyle f(\mathbf {0} )=0.5\left((-2.5)^{2}+(-1)^{2}+(10.472)^{2}\right)=58.456.}  ![{\displaystyle f(\mathbf {0} )=0.5\left((-2.5)^{2}+(-1)^{2}+(10.472)^{2}\right)=58.456.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/08d7cbf06614cc328c0955fd10d2dddeeb5ebe23) 

Now, a suitable      η η   0     {\displaystyle \eta _{0}}  ![{\displaystyle \eta _{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef3886c3f161b7f02d23221bfead21a18ffb82ff) must be found such that

     f  (   x   ( 1 )   )  ≤ ≤  f  (   x   ( 0 )   )  = f (  0  ) .   {\displaystyle f\left(\mathbf {x} ^{(1)}\right)\leq f\left(\mathbf {x} ^{(0)}\right)=f(\mathbf {0} ).}  ![{\displaystyle f\left(\mathbf {x} ^{(1)}\right)\leq f\left(\mathbf {x} ^{(0)}\right)=f(\mathbf {0} ).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b504c9de91de9e0b1dd85a96d8b778dedd84734) 

This can be done with any of a variety of [line search](./Line_search) algorithms. One might also simply guess      η η   0   = 0.001 ,   {\displaystyle \eta _{0}=0.001,}  ![{\displaystyle \eta _{0}=0.001,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/509fb1dafab8b9f14788aca57dd06940dc1066d8) which gives

       x   ( 1 )   =   [    0.0075     0.002     − −  0.20944    ]   .   {\displaystyle \mathbf {x} ^{(1)}={\begin{bmatrix}0.0075\\0.002\\-0.20944\\\end{bmatrix}}.}  ![{\displaystyle \mathbf {x} ^{(1)}={\begin{bmatrix}0.0075\\0.002\\-0.20944\\\end{bmatrix}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/685640a7600f2b9f2b69fc9bbbb1ab448af8a487) 

Evaluating the objective function at this value, yields

     f  (   x   ( 1 )   )  = 0.5  (  ( − −  2.48  )  2   + ( − −  1.00  )  2   + ( 6.28  )  2    )  = 23.306.   {\displaystyle f\left(\mathbf {x} ^{(1)}\right)=0.5\left((-2.48)^{2}+(-1.00)^{2}+(6.28)^{2}\right)=23.306.}  ![{\displaystyle f\left(\mathbf {x} ^{(1)}\right)=0.5\left((-2.48)^{2}+(-1.00)^{2}+(6.28)^{2}\right)=23.306.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/79df72924f1aa4d4fa5886bbd37ee4c9eeb3770b) 

The decrease from     f (  0  ) = 58.456   {\displaystyle f(\mathbf {0} )=58.456}  ![{\displaystyle f(\mathbf {0} )=58.456}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54b4036d6c293c46e7535e2a269d71c1f12ecb31) to the next step's value of

     f  (   x   ( 1 )   )  = 23.306   {\displaystyle f\left(\mathbf {x} ^{(1)}\right)=23.306}  ![{\displaystyle f\left(\mathbf {x} ^{(1)}\right)=23.306}](https://wikimedia.org/api/rest_v1/media/math/render/svg/efa2e84afa98511a87ff55b16480cd5683a98e25) 

is a sizable decrease in the objective function. Further steps would reduce its value further until an approximate solution to the system was found.

 

## Comments

 

Gradient descent works in spaces of any number of dimensions, even in infinite-dimensional ones. In the latter case, the search space is typically a [function space](./Function_space), and one calculates the [Fréchet derivative](./Fréchet_derivative) of the functional to be minimized to determine the descent direction.[[7]](./Gradient_descent#cite_note-AK82-7)

 

That gradient descent works in any number of dimensions (finite number at least) can be seen as a consequence of the [Cauchy–Schwarz inequality](./Cauchy–Schwarz_inequality), i.e. the magnitude of the inner (dot) product of two vectors of any dimension is maximized when they are [colinear](./Colinear). In the case of gradient descent, that would be when the vector of independent variable adjustments is proportional to the gradient vector of partial derivatives.

 

The gradient descent can take many iterations to compute a local minimum with a required [accuracy](./Accuracy), if the [curvature](./Curvature) in different directions is very different for the given function. For such functions, [preconditioning](./Preconditioning), which changes the geometry of the space to shape the function level sets like [concentric circles](./Concentric_circles), cures the slow convergence. Constructing and applying preconditioning can be computationally expensive, however.

 

The gradient descent can be modified via momentums[[16]](./Gradient_descent#cite_note-16) ([Nesterov](./Nesterov), Polyak,[[17]](./Gradient_descent#cite_note-17) and Frank–Wolfe[[18]](./Gradient_descent#cite_note-18)) and heavy-ball parameters (exponential moving averages[[19]](./Gradient_descent#cite_note-19) and positive-negative momentum[[20]](./Gradient_descent#cite_note-20)). The main examples of such optimizers are Adam, DiffGrad, Yogi, AdaBelief, etc.

 

Methods based on [Newton's method](./Newton's_method_in_optimization) and inversion of the [Hessian](./Hessian_matrix) using [conjugate gradient](./Conjugate_gradient) techniques can be better alternatives.[[21]](./Gradient_descent#cite_note-21)[[22]](./Gradient_descent#cite_note-22) Generally, such methods converge in fewer iterations, but the cost of each iteration is higher. An example is the [BFGS method](./Broyden–Fletcher–Goldfarb–Shanno_algorithm) which consists in calculating on every step a matrix by which the gradient vector is multiplied to go into a "better" direction, combined with a more sophisticated [line search](./Line_search) algorithm, to find the "best" value of     η η  .   {\displaystyle \eta .}  ![{\displaystyle \eta .}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fc94fc42a3ecbad87643808e17ec9634147cf812) For extremely large problems, where the computer-memory issues dominate, a limited-memory method such as [L-BFGS](./Limited-memory_BFGS) should be used instead of BFGS or the steepest descent. 

 

While it is sometimes possible to substitute gradient descent for a [local search](./Local_search_(optimization)) algorithm, gradient descent is not in the same family: although it is an [iterative method](./Iterative_method) for [local optimization](./Global_optimization), it relies on an [objective function's gradient](./Loss_function) rather than an explicit exploration of a [solution space](./Feasible_region).

 

Gradient descent can be viewed as applying [Euler's method](./Euler's_method) for solving [ordinary differential equations](./Ordinary_differential_equations)      x ′  ( t ) = − −  ∇ ∇  f ( x ( t ) )   {\displaystyle x'(t)=-\nabla f(x(t))}  ![{\displaystyle x'(t)=-\nabla f(x(t))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f7efd24e9cf34508df8d402a5b9801290acb2afc) to a [gradient flow](./Gradient_flow).  In turn, this equation may be derived as an optimal controller[[23]](./Gradient_descent#cite_note-23) for the control system      x ′  ( t ) = u ( t )   {\displaystyle x'(t)=u(t)}  ![{\displaystyle x'(t)=u(t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/861cfd9214a74c07501a0b53535245f7d96715ec) with     u ( t )   {\displaystyle u(t)}  ![{\displaystyle u(t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b375df3b65d282f8715835dc91ccb22f46993959) given in feedback form     u ( t ) = − −  ∇ ∇  f ( x ( t ) )   {\displaystyle u(t)=-\nabla f(x(t))}  ![{\displaystyle u(t)=-\nabla f(x(t))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f86ee85b8175055e73c54efb92404922a835f7dd).

 


