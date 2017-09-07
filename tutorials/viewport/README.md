
# Visual Viewport 和 Layout Viewport

## 桌面浏览器
我们知道，DOM节点被`<body>`标签包含，`<body>`标签又被`<html>`标签包含，那么`<html>`标签又被谁包含呢？答案是Viewport，Viewport包含`<html>`标签。

Viewport是视口的意思，它的尺寸就是浏览器窗口的CSS尺寸，即浏览器窗口的左上角到浏览器窗口的右下角的CSS尺寸范围，它是以CSS像素单位度量的。如下图所示：

如果页面内容很多，导致出现横向滚动条和纵向滚动条，那Viewport的范围怎么表示呢？此时的Viewport还是浏览器窗口从左上角到右下角的CSS尺寸范围，和滚动条的尺寸范围没有关系。

我们可以通过window.innerWidth/Height属性对获取桌面浏览器的Viewport，也可以通过document.documentElement.clientWidth/Height属性对获取，二者存在细微差别。

document.documentElement.clientWidth/Height属性对不包含滚动条，但是window.innerWidth/Height包含。也就是说，如果页面没有滚动条，那么二者是完全相等的；如果存在滚动条，那么window.innerWidth/Height比document.documentElement.clientWidth/Height要大20px左右（在100%缩放的情况下，滚动条的尺寸大约是17px）。

刚才在谈到Viewport的尺寸的时候，我们一直在强调它是浏览器窗口的**CSS**尺寸范围，它是以CSS像素单位度量的，而不是物理像素。

如果我们通过鼠标滚轮放大了当前页面，比如从100%放大到200%了，Viewport会有什么变化吗？在讨论这个问题之前，我们先讨论另一个概念，像素。

像素可以分为物理像素(Physical Pixel)和CSS像素，物理像素又可称为硬件像素(Hardware Pixel)，它是显卡最终向显示屏幕进行图像输出的最小单位，CSS像素又叫做逻辑像素(Logic Pixel)，它是用来在前端中度量DOM长度的最小单位。大部分普通的PC显示屏是用1CSSpx的尺寸等于1物理像素的尺寸，Mac的Retina屏中1 CSS像素的边长等于2个物理像素的边长，1 CSSpx的尺寸等于4个物理像素的尺寸（2*2）。

此处为简化讨论，我们暂时不考虑Retina屏的情况。假设在100%缩放条件下，我们显示器的1 CSS像素尺寸等于1 物理像素尺寸，我们浏览器窗口的初始尺寸是800px X 600px，即浏览器窗口的初始CSS像素尺寸是800px X 600px，而且物理像素尺寸也是800px X 600px，这种情况下，我们通过window.innerWidth/Height属性对和document.documentElement.clientWidth/Height属性对得到的都是800px X 600px。

如果我们通过鼠标滚轮放大了当前页面，比如从100%放大到200%了，此时1个CSS像素需要2*2个物理像素表示，在放大的过程中，物理像素没有变化，还是800px X 600px，但是CSS像素就不一样了，由于CSS像素的的边长在横向上被扩大了两倍，那么放大后的浏览器窗口只包含800 / 2个CSS像素，即400个CSS像素宽，同样地，浏览器窗口的CSS高度尺寸也变为原来的一半，即300个CSS像素高，放大到200%后，我们通过window.innerWidth/Height属性对和document.documentElement.clientWidth/Height属性对得到的都是400px X 300px，即此时Viewport的尺寸就是400px X 300px。由此可见，页面缩放会导致Viewport尺寸变化。桌面浏览器的Viewport依然等价于浏览器窗口的CSS尺寸，只不过现在浏览器窗口的CSS尺寸变小了。

## 移动浏览器

## 总结
Viewport细分为Visual Viewport和Layout Viewport，都以CSS单位进行度量。

 - Visual Viewport: 任意时刻，浏览器窗口左上角到右下角之间的CSS像素尺寸。通过window.innerWidth/Height度量。
 - Layout Viewport: CSS布局，尤其是百分比宽度，是以layout viewport做为参照系来计算的，通过document.documentElement.clientWidth/Height度量。
   - PC浏览器的Layout Viewport：等于Visual Viewport
   - 移动浏览器的Layout Viewport: 在100%缩放比例下，浏览器窗口左上角到右下角之间的CSS像素尺寸，即100%缩放比例下的Visual Layout尺寸。
