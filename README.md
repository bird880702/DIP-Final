# DIP-Final
    %%fcn_responses.m 
.　　此檔案旨在對fcn的數據進行一些前處理<br> 
.　　他將全部的label減去最小值，再除以(Max-Min)，將處理過後的數值加總成sum，再將所有數值除以sum<br>
.　　↑等於讓label變成機率分布<br> 
.　　產出物為mat_file/fcn_data_212.mat<br> 
 
    %%compute_max_regions.m 
.　　利用mask找尋最大可以用的天空區域(長方形)<br> 
.　　產出物為mat_files/max_rects.mat<br> 
 
    %%compute_descriptors.m
.　　`5.Sky Search`中，將FCN後的產物F進行一個average pooling process，變成直方圖H<br>
.　　↑將圖像分成3x3的網格，提取網格s的直方圖Hs，連結後得到H<br> 
.　　產出物為mat_files/descriptor_212.mat<br> 
 
replace_sky.m
====== 
    function[rough_mask,I_rep,I_ref,ref_region,norm_F,ref_im_name] = replace_sky(file_num)
%output<br> 
----- 
`rough_mask`: 目標圖片的predict_label<br>
`I_rep`: replace後的圖片<br>
`I_ref`: 參考圖片<br>
`ref_region`: 參考圖片的predict_label<br>
`norm_F`: 目標圖片的predict_value，變成機率分布後的變數(14,500,500)<br>
`ref_im_name`: 參考圖片的名字(ex:0005.png)<br> 

%input<br> 
----- 
`file_num`: 修改數字即可(ex:1)<br>
.　　在此function中，會先輸入max_rects和descriptor_212兩個檔案<br>
.　　輸入目標圖像和目標圖像的mask，做了一些之前提過的處理(ex: 機率化、直方化、取得最大天空長方形等)<br>
.　　他會藉由max_rects幫你算放大縮小率比較小的4張圖給你選<br>
