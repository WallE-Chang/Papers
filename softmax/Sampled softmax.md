# Sampled softmax

- From softmax
  $$
  p \left( y _ { t } | y _ { < t } , x \right) = \frac { 1 } { Z } \exp \left\{ \mathbf { w } _ { t } ^ { \top } \phi \left( y _ { t - 1 } , z _ { t } , c _ { t } \right) + b _ { t } \right\} \tag{1} \\ \text  { where }Z = \sum _ { k : y _ { k } \in V } \exp \left\{ \mathbf { w } _ { k } ^ { \top } \phi \left( y _ { t - 1 } , z _ { t } , c _ { t } \right) + b _ { k } \right\}
  $$

- Let us consider the gradient of log-probability of the output in Eq.(1)
  $$
  \begin {array} { l } { \nabla \log p \left( y _ { t } | y _ { < t } , x \right) } \tag{2} \ { = \nabla \mathcal { E } \left( y _ { t } \right) - \sum _ { k : y _ { k } \in V } p \left( y _ { k } | y _ { < t } , x \right) \nabla \mathcal { E } \left( y _ { k } \right)   }   \end{array}
  $$
  $\text{where we define the energy }\mathcal { E } \ \text{as :}  \ \mathcal { E } \left( y _ { j } \right) = \mathbf { w } _ { j } ^ { \top } \phi \left( y _ { j - 1 } , z _ { j } , c _ { j } \right) + b _ { j }$

  

- Then we define
  $$
  \mathbb { E } _ { P } [ \nabla \mathcal { E } ( y ) ]\begin {array} { l } { =\sum _ { k : y _ { k } \in V } p \left( y _ { k } | y _ { < t } , x \right) \nabla \mathcal { E } \left( y _ { k } \right)   }   \end{array} \tag{3}
  $$

  > We can use importance sampling:
  > $$
  > \begin{aligned}\mathbb { E } _ { P } [  f ( x ) ] = & \int f ( x ) p ( x ) d x \\ = & \int f ( x ) \frac { p ( x ) } { g ( x ) } g ( x ) d x \\ = & \int h ( x ) w ( x ) g ( x ) d x \qquad  \text  { where } w \left( x \right) = \frac { f \left( x \right) } { g \left( x  \right) } \text  { is importance weight }\\ \approx& \frac {1} {N} \sum _ { i = 1 } ^ { N } h \left( x _ { i } \right) w \left( x _ { i } \right) \\ = & g(x)\sum _ { i = 1 } ^ { N } h \left( x _ { i } \right) w \left( x _ { i } \right) \qquad  \text  { if  g(x)  is uniform distribution }\end {aligned}
  > $$
  > 

- hence


$$
\mathbb { E } _ { P } [ \nabla \mathcal { E } ( y ) ] \approx \sum _ { k : y _ { k } \in V ^ { \prime } } \frac { \omega _ { k } } { \sum _ { k ^ { \prime } : y _ { k ^ { \prime } } \in V ^ { \prime } } \omega _ { k ^ { \prime } } } \nabla \mathcal { E } \left( y _ { k } \right) \tag{4} \\ \text{where} \ \omega _ { k } = \exp \left\{ \mathcal { E } \left( y _ { k } \right) - \log Q \left( y _ { k } \right) \right\}$​
$$

- addintianl
  $$
  Q _ { i } \left( y _ { k } \right) = \left\{ \begin{array} { l l } { \frac { 1 } { V _ { i } ^ { \prime } | } } & { \text { if } y _ { t } \in V _ { i } ^ { \prime } } \\ { 0 } & { \text { otherwise } } \end{array} \right. \tag{5}
  $$

- take Eq.(5) into Eq.(4)
  $$
  \begin{array} { l } { p \left( y _ { t } | y _ { < t } , x \right) }  { \quad = \quad \frac { \exp \left\{ \mathbf { w } _ { t } ^ { \top } \phi \left( y _ { t - 1 } , z _ { t } , c _ { t } \right) + b _ { t } \right\} } { \sum _ { k : y _ { k } \in V ^ { \prime } } \exp \left\{ \mathbf { w } _ { k } ^ { \top } \phi \left( y _ { t - 1 } , z _ { t } , c _ { t } \right) + b _ { k } \right\} } } \end{array} \tag{6}
  $$
  

