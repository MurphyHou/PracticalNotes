## 1. 图片  
***1. object-fit：fill | contain | cover | none | scale-down***
   
  + contain  
   被替换的内容将被缩放，以在填充元素的内容框时保持其宽高比。 整个对象在填充盒子的同时保留其长宽比，因此如果宽高比与框的宽高比不匹配，该对象将被添加“黑边”。

  + cover
  被替换的内容在保持其宽高比的同时填充元素的整个内容框。如果对象的宽高比与内容框不相匹配，该对象将被剪裁以适应内容框。

  + fill  
    被替换的内容正好填充元素的内容框。整个对象将完全填充此框。如果对象的宽高比与内容框不相匹配，那么该对象将被拉伸以适应内容框。

  + none  
    被替换的内容将保持其原有的尺寸。  

  + scale-down  
    内容的尺寸与 none 或 contain 中的一个相同，取决于它们两个之间谁得到的对象尺寸会更小一些。  

   + object-fit 还有一个配套属性 object-position，它可以控制图片在其内容框中的位置。（类似于 background-position），默认是 object-position: 50% 50%，如果你不希望图片居中展示，可以使用它去改变图片实际展示的 position 。  
      ```
      img {
            width: 150px;
            height: 100px;
            object-fit: cover;
            object-position: 50% 100%;
        }
      ```
## 2. Flex布局
  + ### flex-direction属性：决定主轴的方向（即项目的排列方向）  
    ```
    .box {  
        flex-direction: row | row-reverse | column | column-reverse;  
    }  
    ```
    ***1. row（默认值）：主轴为水平方向，起点在左端。***   
    ***2. row-reverse：主轴为水平方向，起点在右端。***  
    ***3. column：主轴为垂直方向，起点在上沿。***  
    ***4. column-reverse：主轴为垂直方向，起点在下沿。***    
   
  + ### flex-wrap属性：默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
    ```
    .box{
        flex-wrap: nowrap | wrap | wrap-reverse;
    }
    ```
  
  + ### flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
    ```
    .box {
        flex-flow: <flex-direction> || <flex-wrap>;
    }
    ```
  + ### justify-content属性: 定义了项目在主轴上的对齐方式。### 
    ```
    .box {
      justify-content: flex-start | flex-end | center | space-between | space-around;
    }
    ```
    *1. flex-start（默认值）：左对齐*    
    *2. flex-end：右对齐*     
    *3. center： 居中*   
    *4. space-between：两端对齐，项目之间的间隔都相等.*   
    *5. space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。*
      
 + ### align-items属性定义项目在交叉轴上如何对齐。
    ```
      .box {
        align-items: flex-start | flex-end | center | baseline | stretch;
      }
    ```
    *1. flex-start：交叉轴的起点对齐。*  
    *2. flex-end：交叉轴的终点对齐。*  
    *3. center：交叉轴的中点对齐。*  
    *4. baseline: 项目的第一行文字的基线对齐。*  
    *5. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。*  

  + ### align-content属性定义了多根轴线的对齐方式。(适用多行多列)如果项目只有一根轴线，该属性不起作用。###  
    ````
      .box {
        align-content: flex-start | flex-end | center | space-between | space-around | stretch;
      }
    ````
    *1.flex-start：与交叉轴的起点对齐。(左对齐)*  
    *2.flex-end：与交叉轴的终点对齐。（右对齐）*  
    *3.center：与交叉轴的中点对齐。*  
    *4.space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。*
    *5.space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。*
    *6.stretch（默认值）：轴线占满整个交叉轴。*

  > + ### 项目属性（box里面的子元素属性）  
  > 1.  order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。 

  > 2. flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。  
    *如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍*  

  > 3. flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。  
      *如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。*  

  > 4. flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。  
    *它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。* 

  > 5. flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。  
    *该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。*  
    *建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。*  

  > 6. align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。     
    ```
    .item {
        align-self: auto | flex-start | flex-end | center | baseline | stretch;
      }
    ```  
  *该属性可能取6个值，除了auto，其他都与align-items属性完全一致。*
     
