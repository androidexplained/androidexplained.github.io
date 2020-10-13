---
layout: post
title:  "Hexadecimal color code for transparency"
date:   2020-10-12 21:50:30 +0200
categories: android ui
---
During the lifetime of every android developer there comes a time when he has to use color transparency on android.
Whether it's to add an overlay to bring something into focus or simply create an ugly custom view that is a part of business requirements.

In this post we'll cover how the color transparency works on android.

## Understanding color transparency
On android the color can be declared in the following format <br />
#**AA**RRGGBB
* `AA` - is the bit that's of most interest to us in this article, it stands for **alpha** channel
* `RR GG BB` - **red**, **green** & **blue** channels respectively

It is also worth noting that each channel is represented as a hexadecimal number.

Now in order to add transparency to our color we need to prepend it with hexadecimal value representing the alpha (transparency).

For example if you want to set **80%** transparency value to black color (**#000000**) you need to prepend it with **CC**, as a result we end up with the following color resource **#CC000000**.

Below please find a list of all hexadecimal values for 0 to 100% transparency.

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;width: 40%}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-c3ow{border-color:inherit;text-align:center;vertical-align:top}
.tg .tg-dvpl{border-color:inherit;text-align:center;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-dvpl"><b>Transparency</b></th>
    <th class="tg-c3ow"><b>Hex value</b></th>
  </tr>
</thead>
<tbody>
<tr>
  <td class="tg-dvpl">100%</td>
  <td class="tg-c3ow"><span >FF</span></td>
</tr>
  <tr>
    <td class="tg-dvpl">99%</td>
    <td class="tg-c3ow"><span >FC</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">98%</td>
    <td class="tg-c3ow"><span >FA</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">97%</td>
    <td class="tg-c3ow"><span >F7</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">96%</td>
    <td class="tg-c3ow"><span >F5</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">95%</td>
    <td class="tg-c3ow"><span >F2</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">94%</td>
    <td class="tg-c3ow"><span >F0</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">93%</td>
    <td class="tg-c3ow"><span >ED</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">92%</td>
    <td class="tg-c3ow"><span >EB</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">91%</td>
    <td class="tg-c3ow"><span >E8</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">90%</td>
    <td class="tg-c3ow"><span >E6</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">89%</td>
    <td class="tg-c3ow"><span >E3</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">88%</td>
    <td class="tg-c3ow"><span >E0</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">87%</td>
    <td class="tg-c3ow"><span >DE</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">86%</td>
    <td class="tg-c3ow"><span >DB</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">85%</td>
    <td class="tg-c3ow"><span >D9</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">84%</td>
    <td class="tg-c3ow"><span >D6</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">83%</td>
    <td class="tg-c3ow"><span >D4</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">82%</td>
    <td class="tg-c3ow"><span >D1</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">81%</td>
    <td class="tg-c3ow"><span >CF</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">80%</td>
    <td class="tg-c3ow"><span >CC</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">79%</td>
    <td class="tg-c3ow"><span >C9</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">78%</td>
    <td class="tg-c3ow"><span >C7</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">77%</td>
    <td class="tg-c3ow"><span >C4</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">76%</td>
    <td class="tg-c3ow"><span >C2</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">75%</td>
    <td class="tg-c3ow"><span >BF</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">74%</td>
    <td class="tg-c3ow"><span >BD</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">73%</td>
    <td class="tg-c3ow"><span >BA</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">72%</td>
    <td class="tg-c3ow"><span >B8</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">71%</td>
    <td class="tg-c3ow"><span >B5</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">70%</td>
    <td class="tg-c3ow"><span >B3</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">69%</td>
    <td class="tg-c3ow"><span >B0</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">68%</td>
    <td class="tg-c3ow"><span >AD</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">67%</td>
    <td class="tg-c3ow"><span >AB</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">66%</td>
    <td class="tg-c3ow"><span >A8</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">65%</td>
    <td class="tg-c3ow"><span >A6</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">64%</td>
    <td class="tg-c3ow"><span >A3</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">63%</td>
    <td class="tg-c3ow"><span >A1</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">62%</td>
    <td class="tg-c3ow"><span >9E</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">61%</td>
    <td class="tg-c3ow"><span >9C</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">60%</td>
    <td class="tg-c3ow"><span >99</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">59%</td>
    <td class="tg-c3ow"><span >96</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">58%</td>
    <td class="tg-c3ow"><span >94</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">57%</td>
    <td class="tg-c3ow"><span >91</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">56%</td>
    <td class="tg-c3ow"><span >8F</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">55%</td>
    <td class="tg-c3ow"><span >8C</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">54%</td>
    <td class="tg-c3ow"><span >8A</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">53%</td>
    <td class="tg-c3ow"><span >87</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">52%</td>
    <td class="tg-c3ow"><span >85</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">51%</td>
    <td class="tg-c3ow"><span >82</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">50%</td>
    <td class="tg-c3ow"><span >80</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">49%</td>
    <td class="tg-c3ow"><span >7D</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">48%</td>
    <td class="tg-c3ow"><span >7A</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">47%</td>
    <td class="tg-c3ow"><span >78</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">46%</td>
    <td class="tg-c3ow"><span >75</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">45%</td>
    <td class="tg-c3ow"><span >73</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">44%</td>
    <td class="tg-c3ow"><span >70</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">43%</td>
    <td class="tg-c3ow"><span >6E</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">42%</td>
    <td class="tg-c3ow"><span >6B</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">41%</td>
    <td class="tg-c3ow"><span >69</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">40%</td>
    <td class="tg-c3ow"><span >66</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">39%</td>
    <td class="tg-c3ow"><span >63</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">38%</td>
    <td class="tg-c3ow"><span >61</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">37%</td>
    <td class="tg-c3ow"><span >5E</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">36%</td>
    <td class="tg-c3ow"><span >5C</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">35%</td>
    <td class="tg-c3ow"><span >59</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">34%</td>
    <td class="tg-c3ow"><span >57</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">33%</td>
    <td class="tg-c3ow"><span >54</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">32%</td>
    <td class="tg-c3ow"><span >52</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">31%</td>
    <td class="tg-c3ow"><span >4F</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">30%</td>
    <td class="tg-c3ow"><span >4D</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">29%</td>
    <td class="tg-c3ow"><span >4A</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">28%</td>
    <td class="tg-c3ow"><span >47</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">27%</td>
    <td class="tg-c3ow"><span >45</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">26%</td>
    <td class="tg-c3ow"><span >42</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">25%</td>
    <td class="tg-c3ow"><span >40</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">24%</td>
    <td class="tg-c3ow"><span >3D</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">23%</td>
    <td class="tg-c3ow"><span >3B</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">22%</td>
    <td class="tg-c3ow"><span >38</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">21%</td>
    <td class="tg-c3ow"><span >36</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">20%</td>
    <td class="tg-c3ow"><span >33</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">19%</td>
    <td class="tg-c3ow"><span >30</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">18%</td>
    <td class="tg-c3ow"><span >2E</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">17%</td>
    <td class="tg-c3ow"><span >2B</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">16%</td>
    <td class="tg-c3ow"><span >29</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">15%</td>
    <td class="tg-c3ow"><span >26</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">14%</td>
    <td class="tg-c3ow"><span >24</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">13%</td>
    <td class="tg-c3ow"><span >21</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">12%</td>
    <td class="tg-c3ow"><span >1F</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">11%</td>
    <td class="tg-c3ow"><span >1C</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">10%</td>
    <td class="tg-c3ow"><span >1A</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">9%</td>
    <td class="tg-c3ow"><span >17</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">8%</td>
    <td class="tg-c3ow"><span >14</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">7%</td>
    <td class="tg-c3ow"><span >12</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">6%</td>
    <td class="tg-c3ow"><span >0F</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">5%</td>
    <td class="tg-c3ow"><span >0D</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">4%</td>
    <td class="tg-c3ow"><span >0A</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">3%</td>
    <td class="tg-c3ow"><span >08</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">2%</td>
    <td class="tg-c3ow"><span >05</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">1%</td>
    <td class="tg-c3ow"><span >03</span></td>
  </tr>
  <tr>
    <td class="tg-dvpl">0%</td>
    <td class="tg-c3ow"><span >00</span></td>
  </tr>
</tbody>
</table>

In this post we've learned how color transparency works on android.
