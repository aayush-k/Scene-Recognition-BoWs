Aayush Kumar

<html>
<head>
<title>Recognition with Bag of Words</title>
<link href='http://fonts.googleapis.com/css?family=Nunito:300|Crimson+Text|Droid+Sans+Mono' rel='stylesheet' type='text/css'>
<link rel="stylesheet" title="Default" href="styles/github.css">
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script>

<link rel="stylesheet" href="html/highlighting/styles/default.css">
<script src="html/highlighting/highlight.pack.js"></script>

</head>
<body>
<div id="header" >
<div id="headersub">
<h1>Aayush Kumar</h1>
</div>
</div>
<div class="container">

<h2>Project 4 / Scene Recognition with Bag of Words</h2>


<p> 	This project focused on extrapolating the subject labels of images using bags of images. Apart from the original project requirements, I did the following extra credit:</p>

<ol>
<li>Used a Gaussian Pyramid Blur Image before vectorizing feature at sigma = 0.25</li>
<li>Implemented k=10 nearest neighbors instead of nearest neighbor</li>
<li>Experimented with many different vocabulary sizes and report performance. E.g. 10, 20, 50, 100, 200, 400, 1000, 10000..</li>
<!-- 200 = 66.1, 10 = 41.5,  -->
<li>etc.</li>
</ol>

<p> I found this project to be a really cool application of the NLP concept of Bag of Words, something that I didn't realize could be applied to sift features and image interest points. Below are my results and optimal parameters.
Algorithmically I followed the instructions mostly, choosing to do things slightly differently with k nearest neighbors instead of the absolute nearest neighbor as well as applying a Gaussian filter before processing my images.
</p>
<div style="clear:both">

<h2>Tiny Images/Bags of Sift with Nearest Neighbor/1 vs all SVM</h2>

<h3>
Nearest Neighbor:
</h3>
<p>Tiny Image: 0.194</p>
<p>Bag of Sift: 0.423</p>

<h3>
1 vs all SVM:
</h3>
<p>Tiny Image: 0.127</p>
<p>Bag of Sift: 0.661</p>


<h2>Paramter Optimization</h2>
Below are the parameters I tweaked to achieve optimal results

<pre><code>
%Gaussian Pyramid
im = imgaussfilt(im, 0.25);

%SVM Lambda value
lambda = 0.0001;
% 10 =>
% 1 =>
% 0.1 => 0.485
% 0.01 => 0.517
% 0.001 => 0.625
% 0.0001 => 0.622
% 0.00001 => 0.583
% 0.000001 => 0.544

%Vocabulary Size (See table below for confusion matrices)
vocab_size = 200
% 10: Accuracy (mean of diagonal of confusion matrix) is 0.421
% 50: Accuracy (mean of diagonal of confusion matrix) is 0.594
% 100: Accuracy (mean of diagonal of confusion matrix) is 0.623
% 200: Accuracy (mean of diagonal of confusion matrix) is 0.661
% 400: Accuracy (mean of diagonal of confusion matrix) is 0.629
% 1000: Accuracy (mean of diagonal of confusion matrix) is 0.652
% 10000: Accuracy (mean of diagonal of confusion matrix) is 0.686
</code></pre>

<h3>Results in a table</h3>

<table border=0>
<tr>
Vocab Sizes: 10, 50, 100, 1000, 10000
<td>
<img src="html/10BOI/confusion_matrix.png" width="24%"/>
<img src="html/50BOI/confusion_matrix.png"  width="24%"/>
<img src="html/100BOI/confusion_matrix.png" width="24%"/>
</td>

</tr>
<tr>
<td>
<img src="html/100BOI/confusion_matrix.png" width="24%"/>
<img src="html/1000BOI/confusion_matrix.png" width="24%"/>
<img src="html/10000BOI/confusion_matrix.png" width="24%"/>

</td>
</tr>

</table>
<p>

<center>
<h1>Scene classification results visualization</h1>
<img src="html/confusion_matrix.png">

<br>
Accuracy (mean of diagonal of confusion matrix) is 0.661
<p>

<table border=0 cellpadding=4 cellspacing=1>
<tr>
<th>Category name</th>
<th>Accuracy</th>
<th colspan=2>Sample training images</th>
<th colspan=2>Sample true positives</th>
<th colspan=2>False positives with true label</th>
<th colspan=2>False negatives with wrong predicted label</th>
</tr>
<tr>
<td>Kitchen</td>
<td>0.500</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Kitchen_image_0102.jpg" width=98 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Kitchen_image_0063.jpg" width=113 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Kitchen_image_0009.jpg" width=100 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Kitchen_image_0044.jpg" width=90 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/LivingRoom_image_0055.jpg" width=100 height=75><br><small>LivingRoom</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Bedroom_image_0052.jpg" width=103 height=75><br><small>Bedroom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Kitchen_image_0184.jpg" width=100 height=75><br><small>TallBuilding</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Kitchen_image_0120.jpg" width=113 height=75><br><small>Bedroom</small></td>
</tr>
<tr>
<td>Store</td>
<td>0.510</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Store_image_0277.jpg" width=105 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Store_image_0062.jpg" width=100 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Store_image_0047.jpg" width=111 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Store_image_0010.jpg" width=104 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/InsideCity_image_0043.jpg" width=75 height=75><br><small>InsideCity</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/LivingRoom_image_0050.jpg" width=107 height=75><br><small>LivingRoom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Store_image_0043.jpg" width=100 height=75><br><small>Office</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Store_image_0027.jpg" width=100 height=75><br><small>Office</small></td>
</tr>
<tr>
<td>Bedroom</td>
<td>0.460</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Bedroom_image_0051.jpg" width=52 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Bedroom_image_0100.jpg" width=112 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Bedroom_image_0082.jpg" width=121 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Bedroom_image_0168.jpg" width=113 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Office_image_0144.jpg" width=115 height=75><br><small>Office</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/LivingRoom_image_0022.jpg" width=100 height=75><br><small>LivingRoom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Bedroom_image_0053.jpg" width=110 height=75><br><small>Office</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Bedroom_image_0157.jpg" width=90 height=75><br><small>Mountain</small></td>
</tr>
<tr>
<td>LivingRoom</td>
<td>0.430</td>
<td bgcolor=LightBlue><img src="html/thumbnails/LivingRoom_image_0248.jpg" width=100 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/LivingRoom_image_0289.jpg" width=100 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/LivingRoom_image_0140.jpg" width=117 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/LivingRoom_image_0087.jpg" width=100 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0085.jpg" width=81 height=75><br><small>Store</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Bedroom_image_0068.jpg" width=74 height=75><br><small>Bedroom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/LivingRoom_image_0058.jpg" width=101 height=75><br><small>Industrial</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/LivingRoom_image_0083.jpg" width=53 height=75><br><small>Industrial</small></td>
</tr>
<tr>
<td>Office</td>
<td>0.780</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Office_image_0002.jpg" width=110 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Office_image_0195.jpg" width=110 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Office_image_0071.jpg" width=104 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Office_image_0106.jpg" width=121 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Bedroom_image_0053.jpg" width=110 height=75><br><small>Bedroom</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0043.jpg" width=100 height=75><br><small>Store</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Office_image_0169.jpg" width=92 height=75><br><small>Bedroom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Office_image_0108.jpg" width=133 height=75><br><small>Bedroom</small></td>
</tr>
<tr>
<td>Industrial</td>
<td>0.380</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Industrial_image_0284.jpg" width=101 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Industrial_image_0131.jpg" width=53 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Industrial_image_0020.jpg" width=112 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Industrial_image_0069.jpg" width=71 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Bedroom_image_0176.jpg" width=57 height=75><br><small>Bedroom</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Street_image_0064.jpg" width=75 height=75><br><small>Street</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Industrial_image_0084.jpg" width=112 height=75><br><small>Bedroom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Industrial_image_0122.jpg" width=51 height=75><br><small>TallBuilding</small></td>
</tr>
<tr>
<td>Suburb</td>
<td>0.900</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Suburb_image_0204.jpg" width=113 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Suburb_image_0238.jpg" width=113 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Suburb_image_0070.jpg" width=113 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Suburb_image_0102.jpg" width=113 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/InsideCity_image_0139.jpg" width=75 height=75><br><small>InsideCity</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0076.jpg" width=54 height=75><br><small>Store</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Suburb_image_0003.jpg" width=113 height=75><br><small>LivingRoom</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Suburb_image_0074.jpg" width=113 height=75><br><small>OpenCountry</small></td>
</tr>
<tr>
<td>InsideCity</td>
<td>0.540</td>
<td bgcolor=LightBlue><img src="html/thumbnails/InsideCity_image_0101.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/InsideCity_image_0147.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/InsideCity_image_0053.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/InsideCity_image_0002.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/TallBuilding_image_0003.jpg" width=75 height=75><br><small>TallBuilding</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0136.jpg" width=70 height=75><br><small>Store</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/InsideCity_image_0067.jpg" width=75 height=75><br><small>Office</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/InsideCity_image_0052.jpg" width=75 height=75><br><small>Office</small></td>
</tr>
<tr>
<td>TallBuilding</td>
<td>0.740</td>
<td bgcolor=LightBlue><img src="html/thumbnails/TallBuilding_image_0251.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/TallBuilding_image_0315.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/TallBuilding_image_0026.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/TallBuilding_image_0067.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/OpenCountry_image_0060.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/InsideCity_image_0126.jpg" width=75 height=75><br><small>InsideCity</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/TallBuilding_image_0084.jpg" width=75 height=75><br><small>Coast</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/TallBuilding_image_0088.jpg" width=75 height=75><br><small>Forest</small></td>
</tr>
<tr>
<td>Street</td>
<td>0.750</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Street_image_0114.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Street_image_0117.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Street_image_0076.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Street_image_0010.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/OpenCountry_image_0012.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Kitchen_image_0075.jpg" width=107 height=75><br><small>Kitchen</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Street_image_0145.jpg" width=75 height=75><br><small>TallBuilding</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Street_image_0146.jpg" width=75 height=75><br><small>TallBuilding</small></td>
</tr>
<tr>
<td>Highway</td>
<td>0.810</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Highway_image_0227.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Highway_image_0127.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Highway_image_0156.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Highway_image_0105.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Coast_image_0054.jpg" width=75 height=75><br><small>Coast</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0078.jpg" width=107 height=75><br><small>Store</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Highway_image_0022.jpg" width=75 height=75><br><small>Coast</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Highway_image_0015.jpg" width=75 height=75><br><small>TallBuilding</small></td>
</tr>
<tr>
<td>OpenCountry</td>
<td>0.540</td>
<td bgcolor=LightBlue><img src="html/thumbnails/OpenCountry_image_0158.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/OpenCountry_image_0342.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/OpenCountry_image_0005.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/OpenCountry_image_0123.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Highway_image_0034.jpg" width=75 height=75><br><small>Highway</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Industrial_image_0135.jpg" width=77 height=75><br><small>Industrial</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/OpenCountry_image_0008.jpg" width=75 height=75><br><small>Coast</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/OpenCountry_image_0022.jpg" width=75 height=75><br><small>Coast</small></td>
</tr>
<tr>
<td>Coast</td>
<td>0.820</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Coast_image_0224.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Coast_image_0127.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Coast_image_0115.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Coast_image_0072.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/OpenCountry_image_0010.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/OpenCountry_image_0022.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Coast_image_0119.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Coast_image_0024.jpg" width=75 height=75><br><small>OpenCountry</small></td>
</tr>
<tr>
<td>Mountain</td>
<td>0.800</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Mountain_image_0276.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Mountain_image_0151.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Mountain_image_0006.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Mountain_image_0085.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Kitchen_image_0125.jpg" width=114 height=75><br><small>Kitchen</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0028.jpg" width=112 height=75><br><small>Store</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Mountain_image_0087.jpg" width=75 height=75><br><small>Suburb</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Mountain_image_0005.jpg" width=75 height=75><br><small>Coast</small></td>
</tr>
<tr>
<td>Forest</td>
<td>0.960</td>
<td bgcolor=LightBlue><img src="html/thumbnails/Forest_image_0283.jpg" width=75 height=75></td>
<td bgcolor=LightBlue><img src="html/thumbnails/Forest_image_0174.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Forest_image_0107.jpg" width=75 height=75></td>
<td bgcolor=LightGreen><img src="html/thumbnails/Forest_image_0021.jpg" width=75 height=75></td>
<td bgcolor=LightCoral><img src="html/thumbnails/Store_image_0106.jpg" width=85 height=75><br><small>Store</small></td>
<td bgcolor=LightCoral><img src="html/thumbnails/OpenCountry_image_0054.jpg" width=75 height=75><br><small>OpenCountry</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Forest_image_0109.jpg" width=75 height=75><br><small>Mountain</small></td>
<td bgcolor=#FFBB55><img src="html/thumbnails/Forest_image_0117.jpg" width=75 height=75><br><small>Mountain</small></td>
</tr>
<tr>
<th>Category name</th>
<th>Accuracy</th>
<th colspan=2>Sample training images</th>
<th colspan=2>Sample true positives</th>
<th colspan=2>False positives with true label</th>
<th colspan=2>False negatives with wrong predicted label</th>
</tr>
</table>
</center>

<div style="clear:both" >
</div>
</body>
</html>
