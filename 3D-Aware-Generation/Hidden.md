they ignore the geometry constraints between views.



+ geometry constraints 

we need to encourage the model reason about the correct 3D shape.





existing methods only optimize a single view of the generated scene independently and ignore the geometry constraints between views.



suffer from collapsed results under large pose vari- ations or have obvious inconsistent artifacts across view



就想极端情况下，如果只有两个视角，有很多不重合的部分，那么这些不重合的部分就可以随意估计，即使有重合部分，也因为不是完备的信息，而可能估计错。因此足够的数据才能缓解这一问题。





Consequently, the generative model can synthesize reasonable images in some views but produce poor renderings in other views (see Fig. 2).
