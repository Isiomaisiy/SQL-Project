Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT country, city, SUM(CAST(totalTransactionRevenue AS NUMERIC)) AS totalTransactionRevenue
FROM all_sessions
WHERE totalTransactionRevenue IS NOT null AND city is NOT null
GROUP BY country, city
ORDER BY totalTransactionRevenue DESC
LIMIT 1


Answer:
This script returns the country and city with the highest number of total transaction revenues,because the column was created as TEXT data type and cast was used to convert data type to numeric.

"country"	"city"	"totaltransactionrevenue"
"United States"	"San Francisco"	1564320000



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT analytics.fullvisitorid, all_sessions.country, all_sessions.city , cast(AVG(CAST(units_sold AS NUMERIC)) as numeric(6,2)) as AverageQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY analytics.fullvisitorid, all_sessions.country, all_sessions.city
ORDER BY AverageQty DESC



Answer:

The null values were eliminated for city and unit sold

fullvisitorid	country	            city	        averageqty
1869599090210680000	United States	Mountain View	707.29
5033655160631190000	United States	Sunnyvale	167
4739164425580130000	United States	San Jose	115.67
1729388992500820000	United States	San Bruno	100.17
2475309279727820000	United States	Seattle	100
545441176553743000	United States	Mountain View	85
335980904099618000	United States	Mountain View	40.2
9441031549900040000	United States	New York	39.28
4471415710206910000	United States	Mountain View	34.55
5302707794869820000	United States	Mountain View	30
1208935828200120000	United States	Atlanta	25
2079305443218950000	United States	Chicago	15.85
7782965489086950000	United States	New York	12.2
376887178827448000	United States	New York	12
6204463650092780000	United States	Chicago	11.95
7702812510306120000	United States	Seattle	10
9984280233013230000	United States	Austin	9.45
7813149961404840000	United States	Salem	8.57
3839652160313320000	United States	Chicago	7
4120018273259560000	United States	Los Angeles	5.94
4851838287757320000	United States	Nashville	5.5
7615194648567110000	United States	Milpitas	5.33
910504852442385000	United States	Jersey City	5.27
8197879643797710000	United States	Charlotte	5.13
9130111652110090000	United States	San Bruno	5
1210981262976880000	United States	Mountain View	5
6342491657336610000	United States	Mountain View	4.6
3376595227948070000	United States	Pittsburgh	4
9587469740521550000	United States	Mountain View	3.8
3441363583316260000	United States	Paris	3.5
7729298327600930000	United States	Cambridge	3.36
3287424336851490000	Canada	Toronto	3
9031952421951510000	United States	Mountain View	3
8561531404669420000	United States	San Francisco	3
5743146680304420000	United States	Kirkland	2.83
5686190022209270000	United States	Mountain View	2.8
425840463868780000	United States	Sunnyvale	2.78
5610631581931690000	Canada	Toronto	2.5
871198635021622000	United States	Houston	2.5
2099864407370020000	United States	San Francisco	2.38
2101046026582150000	United States	Mountain View	2.38
368133363767522000	United States	Sunnyvale	2.35
8497076298632090000	Canada	Toronto	2.33
826679587040384000	United States	Sunnyvale	2.23
8015915032010690000	United States	Mountain View	2.15
6016781152973560000	United States	New York	2.12
6570785835377430000	United States	Chicago	2
614290240685722000	United States	Sunnyvale	2
5507851936577810000	United States	San Francisco	2
5038849050290780000	United States	New York	2
4198598167104310000	India	Hyderabad	2
7728791342122690000	United States	Sunnyvale	2
9320922789328930000	United States	Mountain View	2
2590088265600780000	United States	New York	2
7570488793141300000	United States	Denver	2
5355700591805930000	United States	Mountain View	2
972584416924093000	United States	Mountain View	2
8545452142273020000	United States	San Francisco	2
2904326699888570000	United States	Chicago	1.86
2462053422667850000	United States	Mountain View	1.75
5103606231973310000	United States	Palo Alto	1.75
281952976428623000	United States	Kirkland	1.7
337565799541099000	Germany	Hamburg	1.67
2742641486650040000	United States	Kirkland	1.67
4774789617305710000	United States	Los Angeles	1.67
8782850138494380000	United States	Seattle	1.6
4511566080962450000	United States	New York	1.5
7898346096626230000	United States	Mountain View	1.5
5165576066744060000	United States	Mountain View	1.5
9544769316645610000	United States	Atlanta	1.5
9913166595926800000	United States	Mountain View	1.5
7687739688073310000	United States	Chicago	1.45
1368203961991990000	United States	Austin	1.43
312563032232212000	United States	Santa Monica	1.4
3421355901436190000	United States	San Jose	1.4
5490104931040200000	Hong Kong	Hong Kong	1.39
579540215609411000	United States	Los Angeles	1.33
9415612863537950000	United States	San Jose	1.33
1193224272987330000	United States	Mountain View	1.3
2958670304005360000	United States	New York	1.29
340244222489597000	United States	Mountain View	1.29
2333755080586000000	United States	Chicago	1.17
365800323147392000	United States	Seattle	1.11
3972825715683900000	United States	Mountain View	1
3978566673741050000	Ireland	Dublin	1
4002562102174640000	United States	Atlanta	1
401452598592009000	United States	San Francisco	1
4163967138563830000	United States	Salem	1
4184563806215810000	United States	Palo Alto	1
4232572181865310000	United States	Austin	1
4252274871821990000	Sweden	Stockholm	1
4271986817425850000	United States	New York	1
4278013019962260000	United States	Mountain View	1
432194944891734000	Hong Kong	Hong Kong	1
4325156382147480000	United States	Sunnyvale	1
4368189598145790000	United States	Ann Arbor	1
4371319639324010000	United States	San Francisco	1
437766465921191000	United States	Palo Alto	1
4389726662464050000	India	Ahmedabad	1
455301884218476000	United States	Austin	1
4651155452509120000	United States	Sunnyvale	1
4674412886011340000	United States	New York	1
4682798612908720000	Israel	Tel Aviv-Yafo	1
4717182891697780000	United States	Mountain View	1
490122484982265000	United Kingdom	London	1
4939012230919090000	United States	Chicago	1
4951978802235160000	United States	Chicago	1
4981377510279090000	United States	Austin	1
5041313067421460000	United States	Palo Alto	1
507781256683519000	United States	Seattle	1
5167538107767500000	United States	Mountain View	1
5172139077716780000	Thailand	Bangkok	1
5236189391502620000	United States	Palo Alto	1
5284500895042210000	United States	Sunnyvale	1
532778920952982000	Chile	Santiago	1
5356399203122140000	United States	Chicago	1
5382447057697670000	United States	San Jose	1
5393487182884920000	United States	Mountain View	1
5421819664804190000	United States	Sunnyvale	1
5452974751383490000	United States	Phoenix	1
5475688458260930000	United States	San Francisco	1
5487531102128440000	United States	Sunnyvale	1
5601210622571140000	South Korea	Seoul	1
5635635846003170000	United States	San Francisco	1
5657677988182300000	United States	New York	1
5737334757493900000	Switzerland	Zurich	1
5834541694120920000	United States	Irvine	1
5860117029906720000	Australia	Sydney	1
5950646697725240000	United States	Mountain View	1
5959005239062150000	Japan	Minato	1
5961512277421230000	United States	Mountain View	1
5995953469560070000	United States	New York	1
6002223751438540000	United States	Sunnyvale	1
6200889011683510000	United States	Fremont	1
6223539301349810000	United States	Mountain View	1
6267685909603030000	United States	Mountain View	1
6277843527924100000	Canada	Toronto	1
6343374529353990000	United States	Detroit	1
6347963431749020000	United States	Sunnyvale	1
6438977628599460000	United States	San Francisco	1
6514843913246390000	United States	Mountain View	1
6576706610885980000	United States	Dallas	1
6623087263467920000	United States	Ann Arbor	1
681345956743814000	United States	Austin	1
693079538830911000	United States	Seattle	1
6932506558415730000	United States	Mountain View	1
6977146550952930000	United States	Mountain View	1
6992025260782300000	United Kingdom	London	1
6993935476816490000	Hong Kong	Hong Kong	1
6997260560132630000	United States	Sunnyvale	1
7157831932438270000	United States	Palo Alto	1
7159265482978730000	United States	Sunnyvale	1
7166721188203410000	United States	New York	1
7255003070849690000	United States	San Bruno	1
7269675755736310000	United States	Palo Alto	1
7380903067583690000	United Kingdom	London	1
7418199702900450000	United States	San Jose	1
7483383458886800000	Australia	Sydney	1
7499829957338490000	United States	Sunnyvale	1
7522971304903480000	United States	Mountain View	1
759913108523269000	United States	Santa Clara	1
7633401264222320000	United States	Mountain View	1
765429657120451000	Indonesia	Jakarta	1
7671147450962710000	United States	Austin	1
7681490372890450000	United States	Mountain View	1
7726742944080550000	United States	San Jose	1
7814675004961720000	Colombia	Bogota	1
7894736386239140000	United States	Mountain View	1
7921241728788570000	United States	Cambridge	1
7954367393399820000	United States	Mountain View	1
7996157716861210000	United States	Chicago	1
8161117182595460000	United States	Los Angeles	1
817680240606134000	United States	Ann Arbor	1
8297316052834610000	United States	San Francisco	1
8555664785763980000	India	Hyderabad	1
856463513443144000	United States	New York	1
8645618706223780000	United States	Mountain View	1
8676743052324540000	United States	Mountain View	1
872409986640206000	Germany	Munich	1
14262055593378300	United States	Milpitas	1
8817890066024170000	United Kingdom	London	1
8900752311342110000	United States	Sunnyvale	1
8946840755894410000	United States	New York	1
9023033431421810000	United States	Atlanta	1
9081512956358090000	United Kingdom	London	1
915050757850492000	United States	Mountain View	1
9225056479434500000	Japan	Yokohama	1
9253891173940030000	United States	San Francisco	1
9268915663800050000	United States	San Francisco	1
9306911300688030000	Uruguay	Montevideo	1
9359260991266220000	United States	San Jose	1
939020494867094000	United States	San Francisco	1
9396270502058510000	Singapore	Singapore	1
9416659624720080000	United States	Sunnyvale	1
943467190650298000	United States	Sunnyvale	1
9453866125712880000	United States	Mountain View	1
9547479182887460000	United States	San Jose	1
9609104828919390000	United States	New York	1
9680035734105240000	United States	Sunnyvale	1
9684421720885920000	United States	Mountain View	1
972040324417630000	United States	Santa Clara	1
9774338255520480000	Spain	Madrid	1
980539649904359000	United States	Austin	1
8726427406034600000	United States	Ann Arbor	1
82784177006211600	United States	New York	1
204396754212287000	Thailand	Bangkok	1
25048695599932300	United States	Mountain View	1
273273778759886000	United States	Chicago	1
277134385518698000	United States	Ann Arbor	1
305653906525013000	United States	South San Francisco	1
311188034141973000	Taiwan	Zhongli District	1
348842070964414000	United States	Mountain View	1
483377965455528000	Germany	Munich	1
551409262432196000	United States	Sunnyvale	1
572816056475383000	Germany	Berlin	1
86102919761743400	United States	Mountain View	1
957309643785473000	United States	Ann Arbor	1
1075676281884860000	United States	Mountain View	1
1076409378746580000	United States	Mountain View	1
118139814032445000	United States	Mountain View	1
1193376245361270000	United States	Mountain View	1
1292268456140740000	United States	San Jose	1
1315772786660600000	United States	Mountain View	1
1373697057662330000	France	Paris	1
1437703405675890000	United States	New York	1
1451317767256580000	United States	Irvine	1
1522616108077050000	United States	New York	1
1563065767696460000	United States	New York	1
1569663514316880000	United States	San Jose	1
1658867631945870000	United States	San Diego	1
173113095050385000	United States	New York	1
1808807059522220000	Switzerland	Zurich	1
1862546724568840000	United States	New York	1
1882171112978890000	United States	San Francisco	1
1953156898351160000	Canada	Kitchener	1
2061706088657700000	United States	New York	1
2071681587677540000	Thailand	Bangkok	1
2111953635618240000	United States	Kirkland	1
2194483396324030000	United States	Mountain View	1
2280491500915670000	United States	Kirkland	1
2310334534790810000	United States	San Bruno	1
2338178303528910000	United States	Sunnyvale	1
238215560062540000	United States	Sunnyvale	1
239171628500742000	United States	Mountain View	1
2518379317255530000	United States	Mountain View	1
2551574846790560000	United States	Sunnyvale	1
2662407820996460000	United States	Mountain View	1
2678202602250260000	Switzerland	Zurich	1
2690535203969670000	Japan	Minato	1
2694014479461830000	United States	Mountain View	1
2870753734955790000	United States	Mountain View	1
2935198745073120000	United States	Chicago	1
294179179450210000	Japan	Osaka	1
294652112012427000	United States	San Jose	1
2972255044152200000	United States	Mountain View	1
297297076536180000	Canada	Toronto	1
299679623448520000	United States	San Francisco	1
3108402817879400000	United States	New York	1
3110501278230390000	United States	Mountain View	1
3212425292937990000	United States	Mountain View	1
321853468075977000	United States	Sunnyvale	1
3227849441375670000	United States	Cupertino	1
3269323091704320000	United States	San Francisco	1
3303063218833420000	United States	New York	1
3347304258797600000	United States	Mountain View	1
3372253426464410000	United States	Mountain View	1
3384404255180450000	United States	Sunnyvale	1
3392274336013900000	United States	Palo Alto	1
3491627829668790000	United States	Mountain View	1
350163692909705000	United States	Atlanta	1
3529092916236930000	France	Courbevoie	1
3541562648791710000	United States	Mountain View	1
3568066398889650000	United States	San Jose	1
3608767567161060000	United States	Mountain View	1
3610679375052200000	United States	Atlanta	1
3617089945560140000	United States	New York	1
370234223902755000	Finland	Helsinki	1
3717170129903080000	United States	Sunnyvale	1
3720747917791230000	United States	Mountain View	1
3726536768472340000	United States	Chicago	1
3751695647639770000	United States	Mountain View	1
3774481916858540000	United States	Sunnyvale	1
3869316809303360000	United States	New York	1
387849079599046000	United States	Mountain View	1
3937673380007660000	United States	San Jose	1
3950872382770860000	United States	Washington	1





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL AND v2ProductCategory IS NOT null
GROUP BY all_sessions.v2ProductCategory, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductCategory




Answer:

There was no recognizable pattern in the types (product categories) of products ordered from visitors in each city and country.

v2productcategory	country	city	totalqty
Home/Apparel/Men's/	Australia	Sydney	1
Home/Apparel/Headgear/	Canada	Kitchener	1
Apparel	Canada	Toronto	24
Home/Apparel/Men's/Men's-T-Shirts/	Canada	Toronto	11
Home/Apparel/Headgear/	Canada	Toronto	7
Home/Bags/	Canada	Toronto	1
Home/Bags/	Chile	Santiago	1
Home/Apparel/Men's/Men's-T-Shirts/	Colombia	Bogota	4
Home/Shop by Brand/	France	Courbevoie	1
Home/Shop by Brand/Android/	France	Paris	1
Home/Office/	Germany	Berlin	1
Home/Drinkware/	Germany	Hamburg	10
Home/Apparel/Headgear/	Germany	Munich	1
Home/Apparel/Men's/Men's-T-Shirts/	Germany	Munich	1
Home/Electronics/Electronics Accessories/	Hong Kong	Hong Kong	86
Home/Shop by Brand/	Hong Kong	Hong Kong	8
Home/Apparel/Men's/Men's-T-Shirts/	Hong Kong	Hong Kong	1
Home/Accessories/Stickers/	India	Hyderabad	2
Home/Electronics/Audio/	India	Hyderabad	1
Home/Shop by Brand/Android/	Indonesia	Jakarta	1
Home/Bags/	Ireland	Dublin	1
Home/Apparel/Men's/Men's-T-Shirts/	Israel	Tel Aviv-Yafo	1
Home/Apparel/Headgear/	Japan	Minato	6
Home/Office/	Japan	Minato	1
Home/Apparel/Kid's/Kid's-Infant/	Japan	Osaka	2
Home/Shop by Brand/Google/	Japan	Yokohama	6
Home/Apparel/	South Korea	Seoul	2
Home/Drinkware/Mugs and Cups/	Sweden	Stockholm	1
Home/Apparel/Men's/Men's-T-Shirts/	Switzerland	Zurich	2
Home/Accessories/Stickers/	Switzerland	Zurich	1
Home/Electronics/	Switzerland	Zurich	1
Home/Drinkware/	Thailand	Bangkok	2
Home/Bags/	Thailand	Bangkok	1
Home/Bags/	United Kingdom	London	3
Home/Office/Notebooks & Journals/	United Kingdom	London	1
Home/Electronics/	United States	Ann Arbor	25
Home/Apparel/Men's/Men's-T-Shirts/	United States	Ann Arbor	16
Home/Accessories/	United States	Ann Arbor	12
Home/Apparel/Women's/Women's-T-Shirts/	United States	Ann Arbor	1
Home/Drinkware/	United States	Atlanta	25
Home/Apparel/Kid's/	United States	Atlanta	4
Home/Shop by Brand/	United States	Atlanta	3
Home/Apparel/Men's/Men's-T-Shirts/	United States	Atlanta	1
Home/Bags/	United States	Atlanta	1
Home/Shop by Brand/Google/	United States	Atlanta	1
Home/Office/Notebooks & Journals/	United States	Austin	104
Home/Drinkware/Water Bottles and Tumblers/	United States	Austin	10
Home/Bags/Backpacks/	United States	Austin	7
Home/Drinkware/Mugs and Cups/	United States	Austin	2
Home/Electronics/	United States	Austin	2
Home/Nest/Nest-USA/	United States	Austin	2
Home/Apparel/Men's/Men's-Performance Wear/	United States	Austin	1
Home/Office/	United States	Austin	1
Home/Electronics/Electronics Accessories/	United States	Cambridge	47
Home/Apparel/Men's/Men's-T-Shirts/	United States	Cambridge	4
Home/Bags/	United States	Charlotte	426
Home/Apparel/	United States	Chicago	206
Home/Shop by Brand/	United States	Chicago	206
Home/Shop by Brand/YouTube/	United States	Chicago	46
Home/Nest/Nest-USA/	United States	Chicago	18
Home/Electronics/	United States	Chicago	10
Home/Office/Writing Instruments/	United States	Chicago	7
Nest-USA	United States	Chicago	6
Apparel	United States	Chicago	3
Home/Apparel/Women's/Women's-Outerwear/	United States	Chicago	3
Home/Bags/	United States	Chicago	2
Home/Apparel/Men's/Men's-T-Shirts/	United States	Chicago	1
Home/Nest/Nest-USA/	United States	Cupertino	1
Home/Shop by Brand/YouTube/	United States	Dallas	1
Home/Apparel/Headgear/	United States	Denver	6
Drinkware	United States	Detroit	1
Home/Nest/Nest-USA/	United States	Fremont	3
Home/Apparel/Men's/Men's-T-Shirts/	United States	Irvine	4
Home/Bags/Backpacks/	United States	Jersey City	58
Home/Apparel/Women's/	United States	Kirkland	34
Home/Apparel/Men's/Men's-T-Shirts/	United States	Kirkland	17
Home/Office/	United States	Kirkland	10
Home/Apparel/Women's/Women's-T-Shirts/	United States	Kirkland	5
Home/Drinkware/Water Bottles and Tumblers/	United States	Kirkland	3
Home/Electronics/	United States	Los Angeles	107
Home/Nest/Nest-USA/	United States	Los Angeles	25
Home/Apparel/	United States	Los Angeles	4
Home/Apparel/Men's/Men's-T-Shirts/	United States	Los Angeles	4
Home/Apparel/Women's/Women's-T-Shirts/	United States	Milpitas	18
Home/Nest/Nest-USA/	United States	Milpitas	16
Home/Accessories/Stickers/	United States	Mountain View	4975
Home/Accessories/	United States	Mountain View	385
Home/Spring Sale!/	United States	Mountain View	201
Home/Nest/Nest-USA/	United States	Mountain View	180
Home/Electronics/	United States	Mountain View	103
Home/Lifestyle/	United States	Mountain View	30
Home/Apparel/Men's/Men's-T-Shirts/	United States	Mountain View	22
Home/Drinkware/	United States	Mountain View	14
Home/Apparel/Men's/Men's-Outerwear/	United States	Mountain View	13
Home/Bags/	United States	Mountain View	13
Home/Electronics/Audio/	United States	Mountain View	11
Home/Shop by Brand/Google/	United States	Mountain View	10
Home/Accessories/Housewares/	United States	Mountain View	9
Waze	United States	Mountain View	9
Apparel	United States	Mountain View	7
Home/Apparel/Kid's/Kid's-Toddler/	United States	Mountain View	7
Home/Apparel/Women's/Women's-Outerwear/	United States	Mountain View	7
Home/Electronics/Electronics Accessories/	United States	Mountain View	7
Home/Clearance Sale/	United States	Mountain View	6
Home/Electronics/Flashlights/	United States	Mountain View	5
Home/Office/	United States	Mountain View	5
Home/Bags/More Bags/	United States	Mountain View	4
Home/Apparel/Women's/Women's-Performance Wear/	United States	Mountain View	3
Home/Bags/Shopping and Totes/	United States	Mountain View	3
Home/Apparel/Kid's/Kid's-Infant/	United States	Mountain View	2
Home/Apparel/Women's/Women's-T-Shirts/	United States	Mountain View	2
Home/Accessories/Fun/	United States	Mountain View	1
Home/Apparel/Headgear/	United States	Mountain View	1
Home/Apparel/Men's/	United States	Mountain View	1
Home/Shop by Brand/Android/	United States	Mountain View	1
Nest-USA	United States	Nashville	11
Home/Electronics/	United States	New York	67
Home/Office/Writing Instruments/	United States	New York	61
Home/Apparel/Kid's/Kid's-Toddler/	United States	New York	23
Home/Nest/Nest-USA/	United States	New York	15
Home/Apparel/Headgear/	United States	New York	14
Home/Shop by Brand/	United States	New York	14
Home/Shop by Brand/Google/	United States	New York	7
Home/Accessories/Pet/	United States	New York	6
Home/Bags/Backpacks/	United States	New York	6
Home/Office/	United States	New York	5
Home/Apparel/Men's/Men's-Performance Wear/	United States	New York	4
Home/Apparel/Women's/	United States	New York	3
Home/Accessories/Drinkware/	United States	New York	1
Home/Apparel/Kid's/Kid's-Infant/	United States	New York	1
Home/Apparel/Kid's/Kids-Youth/	United States	New York	1
Home/Apparel/Women's/Women's-T-Shirts/	United States	New York	1
Home/Electronics/Audio/	United States	New York	1
Home/Electronics/Electronics Accessories/	United States	New York	1
Home/Shop by Brand/YouTube/	United States	New York	1
Home/Nest/Nest-USA/	United States	Palo Alto	20
Nest-USA	United States	Palo Alto	3
Home/Apparel/Men's/Men's-T-Shirts/	United States	Palo Alto	1
Home/Apparel/Women's/Women's-Outerwear/	United States	Paris	14
Home/Apparel/Men's/	United States	Phoenix	1
Home/Office/Notebooks & Journals/	United States	Pittsburgh	8
Home/Apparel/Men's/Men's-Outerwear/	United States	Salem	197
Home/Apparel/Kid's/Kid's-Toddler/	United States	Salem	3
Home/Shop by Brand/YouTube/	United States	San Bruno	1202
Home/Electronics/Audio/	United States	San Bruno	15
Home/Bags/	United States	San Bruno	6
Home/Accessories/Stickers/	United States	San Diego	1
Home/Nest/Nest-USA/	United States	San Francisco	25
Home/Apparel/Women's/Women's-T-Shirts/	United States	San Francisco	19
Home/Accessories/Fun/	United States	San Francisco	5
Home/Apparel/Men's/Men's-T-Shirts/	United States	San Francisco	5
Home/Shop by Brand/Android/	United States	San Francisco	5
Home/Electronics/Audio/	United States	San Francisco	2
Home/Apparel/Kid's/Kid's-Infant/	United States	San Francisco	1
Home/Drinkware/Water Bottles and Tumblers/	United States	San Francisco	1
Home/Office/	United States	San Francisco	1
Nest-USA	United States	San Francisco	1
Home/Drinkware/Water Bottles and Tumblers/	United States	San Jose	347
Home/Nest/Nest-USA/	United States	San Jose	10
Home/Accessories/Housewares/	United States	San Jose	8
Home/Electronics/Audio/	United States	San Jose	4
Home/Apparel/Men's/Men's-Outerwear/	United States	San Jose	3
Home/Apparel/Kid's/	United States	San Jose	2
Home/Apparel/Men's/Men's-T-Shirts/	United States	San Jose	2
Home/Lifestyle/	United States	San Jose	2
Home/Apparel/	United States	San Jose	1
Home/Electronics/	United States	Santa Clara	3
Home/Accessories/Fun/	United States	Santa Clara	1
Home/Bags/	United States	Santa Monica	7
Home/Accessories/Fun/	United States	Seattle	100
Home/Apparel/Men's/Men's-Outerwear/	United States	Seattle	20
Home/Drinkware/Mugs and Cups/	United States	Seattle	20
Home/Apparel/Men's/Men's-T-Shirts/	United States	Seattle	12
Home/Nest/Nest-USA/	United States	Seattle	8
Home/Apparel/Headgear/	United States	Seattle	4
Home/Bags/Backpacks/	United States	South San Francisco	6
Home/Office/Notebooks & Journals/	United States	Sunnyvale	502
Housewares	United States	Sunnyvale	127
Home/Nest/Nest-USA/	United States	Sunnyvale	37
Home/Apparel/Men's/Men's-Performance Wear/	United States	Sunnyvale	29
Home/Apparel/	United States	Sunnyvale	19
Home/Apparel/Men's/Men's-T-Shirts/	United States	Sunnyvale	12
Home/Accessories/	United States	Sunnyvale	9
Home/Electronics/	United States	Sunnyvale	8
Home/Bags/Backpacks/	United States	Sunnyvale	7
Home/Drinkware/Water Bottles and Tumblers/	United States	Sunnyvale	4
Home/Apparel/Women's/Women's-Outerwear/	United States	Sunnyvale	3
Home/Apparel/Women's/Women's-T-Shirts/	United States	Sunnyvale	3
Home/Bags/	United States	Sunnyvale	3
Home/Apparel/Men's/Men's-Outerwear/	United States	Sunnyvale	1
Home/Apparel/Kid's/Kid's-Infant/	United States	Washington	1
Home/Apparel/Men's/Men's-T-Shirts/	Uruguay	Montevideo	1






**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT all_sessions.v2ProductName, all_sessions.country, all_sessions.city , SUM(CAST(units_sold AS NUMERIC)) as TotalQty
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE units_sold IS NOT null AND city IS NOT NULL
GROUP BY all_sessions.v2ProductName, all_sessions.country, all_sessions.city
ORDER BY all_sessions.country, all_sessions.city, TotalQty desc, all_sessions.v2ProductName


Answer:

There was no regonizable pattern worthy of noting in the product sold.

v2productname	country	city	totalqty
Google Men's Vintage Tank	Australia	Sydney	1
Google Women's Short Sleeve Hero Tee Sky Blue	Australia	Sydney	1
Google 5-Panel Cap	Canada	Kitchener	1
Google Men's 3/4 Sleeve Raglan Henley Grey	Canada	Toronto	24
Google Men's Vintage Tank	Canada	Toronto	10
Android Stretch Fit Hat Black	Canada	Toronto	7
Google Men's 100% Cotton Short Sleeve Hero Tee White	Canada	Toronto	1
Sport Bag	Canada	Toronto	1
Sport Bag	Chile	Santiago	1
YouTube Men's 3/4 Sleeve Henley	Colombia	Bogota	4
Android Onesie Gold	Finland	Helsinki	3
Android Wool Heather Cap Heather/Black	France	Courbevoie	1
Android Lunch Kit	France	Paris	1
Google Doodle Decal	Germany	Berlin	1
22 oz YouTube Bottle Infuser	Germany	Hamburg	10
Google Men's 100% Cotton Short Sleeve Hero Tee Red	Germany	Munich	1
Google Twill Cap	Germany	Munich	1
Google Device Stand	Hong Kong	Hong Kong	86
Waze Pack of 9 Decal Set	Hong Kong	Hong Kong	8
Android Men's Long Sleeve Badge Crew Tee Heather	Hong Kong	Hong Kong	1
Google Youth Short Sleeve T-shirt Royal Blue	India	Ahmedabad	1
Keyboard DOT Sticker	India	Hyderabad	2
Google Bongo Cupholder Bluetooth Speaker	India	Hyderabad	1
Windup Android	Indonesia	Jakarta	1
Google Laptop Backpack	Ireland	Dublin	1
Google Men's Vintage Tank	Israel	Tel Aviv-Yafo	1
Google 5-Panel Snapback Cap	Japan	Minato	6
YouTube Leatherette Notebook Combo	Japan	Minato	1
Google Infant Short Sleeve Tee Red	Japan	Osaka	2
Google Rucksack	Japan	Yokohama	6
Google Men's Short Sleeve Performance Badge Tee Navy	Singapore	Singapore	1
Waze Dress Socks	South Korea	Seoul	2
NestÂ® Protect Smoke + CO White Wired Alarm-USA	Spain	Madrid	1
Android Rise 14 oz Mug	Sweden	Stockholm	1
YouTube Men's 3/4 Sleeve Henley	Switzerland	Zurich	2
Rocket Flashlight	Switzerland	Zurich	1
Waze Mood Ninja Window Decal	Switzerland	Zurich	1
Spiral Notebook and Pen Set	Taiwan	Zhongli District	1
26 oz Double Wall Insulated Bottle	Thailand	Bangkok	1
Foam Can and Bottle Cooler	Thailand	Bangkok	1
Waterproof Backpack	Thailand	Bangkok	1
Android Sticker Sheet Ultra Removable	United Kingdom	London	2
Google Men's Lightweight Microfleece Jacket Black	United Kingdom	London	2
Google Rucksack	United Kingdom	London	2
Android Hard Cover Journal	United Kingdom	London	1
Google Tote Bag	United Kingdom	London	1
Recycled Mouse Pad	United States	Ann Arbor	22
Google Men's Vintage Tank	United States	Ann Arbor	13
Yoga Block	United States	Ann Arbor	12
Google Men's Vintage Badge Tee Black	United States	Ann Arbor	3
Keyboard DOT Sticker	United States	Ann Arbor	3
Google Women's Scoop Neck Tee White	United States	Ann Arbor	1
20 oz Stainless Steel Insulated Tumbler	United States	Atlanta	25
Google Onesie Green	United States	Atlanta	4
Waterproof Backpack	United States	Atlanta	3
Android Men's Vintage Henley	United States	Atlanta	1
Google Alpine Style Backpack	United States	Atlanta	1
Google Rucksack	United States	Atlanta	1
YouTube RFID Journal	United States	Austin	104
Google 25 oz Red Stainless Steel Bottle	United States	Austin	10
25L Classic Rucksack	United States	Austin	7
Compact Selfie Stick	United States	Austin	2
NestÂ® Learning Thermostat 3rd Gen-USA - Copper	United States	Austin	2
Red Shine 15 oz Mug	United States	Austin	2
Google Men's Airflow 1/4 Zip Pullover Black	United States	Austin	1
Switch Tone Color Crayon Pen	United States	Austin	1
Galaxy Screen Cleaning Cloth	United States	Cambridge	47
YouTube Men's Vintage Henley	United States	Cambridge	4
Google Lunch Bag	United States	Charlotte	426
NestÂ® Learning Thermostat 3rd Gen-USA - Copper	United States	Chicago	232
Google Alpine Style Backpack	United States	Chicago	206
Google Men's 100% Cotton Short Sleeve Hero Tee White	United States	Chicago	206
YouTube Custom Decals	United States	Chicago	48
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	Chicago	13
Google Flashlight	United States	Chicago	7
Switch Tone Color Crayon Pen	United States	Chicago	7
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	Chicago	6
Google Women's 1/4 Zip Performance Pullover Black	United States	Chicago	3
Google Womens 3/4 Sleeve Baseball Raglan Heather/Black	United States	Chicago	3
Suitcase Organizer Cubes	United States	Chicago	2
Google Men's Vintage Badge Tee Sage	United States	Chicago	1
YouTube Men's Short Sleeve Hero Tee White	United States	Chicago	1
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	Cupertino	1
YouTube Leatherette Notebook Combo	United States	Dallas	1
Google Twill Cap	United States	Denver	6
Google 22 oz Water Bottle	United States	Detroit	1
NestÂ® Protect Smoke + CO White Battery Alarm-USA	United States	Fremont	3
Google Sunglasses	United States	Houston	5
Google Men's Vintage Badge Tee Sage	United States	Irvine	4
Google Women's Convertible Vest-Jacket Sea Foam Green	United States	Irvine	1
Google Laptop Tech Backpack	United States	Jersey City	58
Google Women's Long Sleeve Tee Lavender	United States	Kirkland	34
Google Men's Vintage Badge Tee Sage	United States	Kirkland	17
Android Sticker Sheet Ultra Removable	United States	Kirkland	10
Google Women's Short Sleeve Badge Tee Grey	United States	Kirkland	5
Google 22 oz Water Bottle	United States	Kirkland	3
Basecamp Explorer Powerbank Flashlight	United States	Los Angeles	107
NestÂ® Cam Indoor Security Camera - USA	United States	Los Angeles	25
Google Bib Red	United States	Los Angeles	4
Google Men's Short Sleeve Hero Tee Heather	United States	Los Angeles	4
Google Women's Short Sleeve Hero Dark Grey	United States	Milpitas	18
NestÂ® Protect Smoke + CO Black Battery Alarm-USA	United States	Milpitas	16
Waze Baby on Board Window Decal	United States	Mountain View	4975
Google Device Stand	United States	Mountain View	380
Grip Highlighter Pen 3 Pack	United States	Mountain View	201
Google Water Resistant Bluetooth Speaker	United States	Mountain View	85
NestÂ® Cam Indoor Security Camera - USA	United States	Mountain View	64
NestÂ® Protect Smoke + CO White Battery Alarm-USA	United States	Mountain View	60
Sport Bag	United States	Mountain View	31
NestÂ® Learning Thermostat 3rd Gen-USA - White	United States	Mountain View	27
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	Mountain View	20
26 oz Double Wall Insulated Bottle	United States	Mountain View	19
Google 25 oz Blue Stainless Steel Bottle	United States	Mountain View	14
Rocket Flashlight	United States	Mountain View	14
Google Zipper-front Sports Bag	United States	Mountain View	13
Google Car Clip Phone Holder	United States	Mountain View	12
Android Luggage Tag	United States	Mountain View	9
Waze Mobile Phone Vent Mount	United States	Mountain View	9
NestÂ® Learning Thermostat 3rd Gen-USA - Copper	United States	Mountain View	8
Google Bib Red	United States	Mountain View	7
Google Device Holder Sticky Pad	United States	Mountain View	7
Google Men's Vintage Badge Tee Black	United States	Mountain View	7
Google Men's Vintage Badge Tee Sage	United States	Mountain View	7
Aluminum Handy Emergency Flashlight	United States	Mountain View	6
Google Bluetooth Headphones	United States	Mountain View	6
1 oz Hand Sanitizer	United States	Mountain View	5
Android Women's Fleece Hoodie	United States	Mountain View	5
Google Bluetooth Speaker-Power Bank	United States	Mountain View	5
Google Men's 100% Cotton Short Sleeve Hero Tee Navy	United States	Mountain View	5
Google Men's 100% Cotton Short Sleeve Hero Tee Red	United States	Mountain View	5
Google Men's Quilted Insulated Vest Black	United States	Mountain View	5
Android Spiral Journal with Pen	United States	Mountain View	4
Google Men's Watershed Full Zip Hoodie Grey	United States	Mountain View	4
Google Vintage Henley Grey/Black	United States	Mountain View	4
NestÂ® Cam Outdoor Security Camera - USA	United States	Mountain View	4
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	Mountain View	4
Compact Selfie Stick	United States	Mountain View	3
Google 17oz Stainless Steel Sport Bottle	United States	Mountain View	3
Google Canvas Tote Natural/Navy	United States	Mountain View	3
Google Men's Airflow 1/4 Zip Pullover Lapis	United States	Mountain View	3
Google Men's Bike Short Sleeve Tee Charcoal	United States	Mountain View	3
Google Women's Performance Full Zip Jacket Black	United States	Mountain View	3
NestÂ® Learning Thermostat 3rd Gen-USA	United States	Mountain View	3
UpCycled Handlebar Bag	United States	Mountain View	3
Android Infant Short Sleeve Tee Pewter	United States	Mountain View	2
Android Men's Engineer Short Sleeve Tee Charcoal	United States	Mountain View	2
Google Men's 100% Cotton Short Sleeve Hero Tee White	United States	Mountain View	2
Google Women's Quilted Insulated Vest Black	United States	Mountain View	2
Google Women's Short Sleeve Hero Tee Black	United States	Mountain View	2
Google Women's Short Sleeve Hero Tee Sky Blue	United States	Mountain View	2
Android Rise 14 oz Mug	United States	Mountain View	1
Android Sticker Sheet Ultra Removable	United States	Mountain View	1
Google Men's Performance 1/4 Zip Pullover Heather/Black	United States	Mountain View	1
Google Snapback Hat Black	United States	Mountain View	1
Google Sunglasses	United States	Mountain View	1
Google Twill Cap	United States	Mountain View	1
Google Women's Convertible Vest-Jacket Black	United States	Mountain View	1
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	Nashville	11
Collapsible Shopping Bag	United States	New York	1139
Metal Texture Roller Pen	United States	New York	61
Keyboard DOT Sticker	United States	New York	55
You Tube Toddler Short Sleeve Tee Red	United States	New York	22
Google Women's Lightweight Microfleece Jacket	United States	New York	19
Compact Bluetooth Speaker	United States	New York	12
Google Hard Cover Journal	United States	New York	12
Google Twill Cap	United States	New York	9
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	New York	8
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	New York	7
Google Pet Feeding Mat	United States	New York	6
Waterproof Backpack	United States	New York	6
Android Rise 14 oz Mug	United States	New York	5
Google Bluetooth Speaker-Power Bank	United States	New York	5
Google Snapback Hat Black	United States	New York	5
Google Trucker Hat	United States	New York	5
Seat Pack Organizer	United States	New York	5
Google Men's Short Sleeve Performance Badge Tee Pewter	United States	New York	4
Google Laptop and Cell Phone Stickers	United States	New York	3
Google Women's Vintage Hero Tee Platinum	United States	New York	3
Google Women's Convertible Vest-Jacket Sea Foam Green	United States	New York	2
16 oz. Hot and Cold Tumbler	United States	New York	1
Android Infant Short Sleeve Tee Pewter	United States	New York	1
Google Toddler Sports T-shirt Red	United States	New York	1
Google Water Resistant Bluetooth Speaker	United States	New York	1
Google Women's Recycled Fabric Tee	United States	New York	1
Google Youth Short Sleeve T-shirt Yellow	United States	New York	1
Recycled Mouse Pad	United States	New York	1
Red Spiral Google Notebook	United States	New York	1
YouTube Women's Short Sleeve Tri-blend Badge Tee Grey	United States	New York	1
NestÂ® Cam Outdoor Security Camera - USA	United States	Palo Alto	9
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	Palo Alto	7
NestÂ® Learning Thermostat 3rd Gen-USA - White	United States	Palo Alto	7
YouTube Men's Skater Tee Charcoal	United States	Palo Alto	1
Google Women's Quilted Insulated Vest Black	United States	Paris	14
Google Men's Short Sleeve Hero Tee Heather	United States	Phoenix	1
YouTube Hard Cover Journal	United States	Pittsburgh	8
Google Men's  Zip Hoodie	United States	Salem	197
Google Toddler Hoodie Royal Blue	United States	Salem	3
22 oz YouTube Bottle Infuser	United States	San Bruno	1202
Google G Noise-reducing Bluetooth Headphones	United States	San Bruno	15
Large Zipper Top Tote Bag	United States	San Bruno	6
Google Men's Long Sleeve Raglan Ocean Blue	United States	San Bruno	2
Google Doodle Decal	United States	San Diego	1
Google Women's Scoop Neck Tee White	United States	San Francisco	19
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	San Francisco	15
Windup Android	United States	San Francisco	10
Google Men's Short Sleeve Hero Tee Light Blue	United States	San Francisco	8
Google Snapback Hat Black	United States	San Francisco	8
NestÂ® Cam Outdoor Security Camera - USA	United States	San Francisco	5
Android Men's Long Sleeve Badge Crew Tee Heather	United States	San Francisco	4
Google Women's 3/4 Sleeve Baseball Raglan Heather/Black	United States	San Francisco	4
Google Women's Yoga Pants	United States	San Francisco	4
NestÂ® Learning Thermostat 3rd Gen-USA - Copper	United States	San Francisco	4
Micro Wireless Earbud	United States	San Francisco	2
NestÂ® Protect Smoke + CO White Battery Alarm-USA	United States	San Francisco	2
Android Hard Cover Journal	United States	San Francisco	1
Android Onesie Gold	United States	San Francisco	1
Google 22 oz Water Bottle	United States	San Francisco	1
Google Vintage Henley Grey/Black	United States	San Francisco	1
22 oz Android Bottle	United States	San Jose	347
Google Lunch Bag	United States	San Jose	8
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	San Jose	7
Google Bongo Cupholder Bluetooth Speaker	United States	San Jose	4
NestÂ® Protect Smoke + CO White Battery Alarm-USA	United States	San Jose	3
Crunch-It Dog Toy	United States	San Jose	2
Google Bib Red	United States	San Jose	2
Google Men's  Zip Hoodie	United States	San Jose	2
Google Women's Short Sleeve Hero Tee White	United States	San Jose	2
YouTube Men's Vintage Tank	United States	San Jose	2
Google 5-Panel Cap	United States	San Jose	1
Google Men's Pullover Hoodie Grey	United States	San Jose	1
Clip-on Compact Charger	United States	Santa Clara	3
Android Luggage Tag	United States	Santa Clara	1
Google Slim Utility Travel Bag	United States	Santa Monica	7
Google Luggage Tag	United States	Seattle	100
Android Men's  Zip Hoodie	United States	Seattle	20
Android Rise 14 oz Mug	United States	Seattle	20
Android Men's Vintage Henley	United States	Seattle	12
NestÂ® Cam Indoor Security Camera - USA	United States	Seattle	8
Android Twill Cap	United States	Seattle	4
Google Rucksack	United States	South San Francisco	6
Google Hard Cover Journal	United States	Sunnyvale	501
SPF-15 Slim & Slender Lip Balm	United States	Sunnyvale	127
Google Men's Convertible Vest-Jacket Pewter	United States	Sunnyvale	29
NestÂ® Protect Smoke + CO White Wired Alarm-USA	United States	Sunnyvale	25
Google Men's Pullover Hoodie Grey	United States	Sunnyvale	12
YouTube Men's Short Sleeve Hero Tee Charcoal	United States	Sunnyvale	9
Android Lunch Kit	United States	Sunnyvale	7
Google Men's 100% Cotton Short Sleeve Hero Tee White	United States	Sunnyvale	7
Waterproof Backpack	United States	Sunnyvale	6
Electronics Accessory Pouch	United States	Sunnyvale	5
NestÂ® Learning Thermostat 3rd Gen-USA - Stainless Steel	United States	Sunnyvale	5
Google 17oz Stainless Steel Sport Bottle	United States	Sunnyvale	4
NestÂ® Cam Indoor Security Camera - USA	United States	Sunnyvale	4
Collapsible Shopping Bag	United States	Sunnyvale	3
Google 4400mAh Power Bank	United States	Sunnyvale	3
Android Men's Vintage Henley	United States	Sunnyvale	2
Google Women's Convertible Vest-Jacket Sea Foam Green	United States	Sunnyvale	2
Google Women's Recycled Fabric Tee	United States	Sunnyvale	2
Seat Pack Organizer	United States	Sunnyvale	2
Android Women's Fleece Hoodie	United States	Sunnyvale	1
Google Alpine Style Backpack	United States	Sunnyvale	1
Google Men's Microfiber 1/4 Zip Pullover Blue/Indigo	United States	Sunnyvale	1
Google Men's Vintage Badge Tee Sage	United States	Sunnyvale	1
Google Metallic Notebook Set	United States	Sunnyvale	1
Google Women's Vintage Hero Tee Lavender	United States	Sunnyvale	1
NestÂ® Cam Outdoor Security Camera - USA	United States	Sunnyvale	1
NestÂ® Learning Thermostat 3rd Gen-USA - Copper	United States	Sunnyvale	1
NestÂ® Protect Smoke + CO White Battery Alarm-USA	United States	Sunnyvale	1
Google Bib White	United States	Washington	1
Google Vintage Henley Grey/Black	Uruguay	Montevideo	1






**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

with cte as (
SELECT all_sessions.country, all_sessions.city , SUM(CAST(revenue AS NUMERIC)) as TotalRevenue
FROM all_sessions
JOIN analytics ON analytics.fullvisitorid = all_sessions.fullvisitorid
WHERE revenue IS NOT null AND city IS NOT NULL
GROUP BY all_sessions.country, all_sessions.city
--ORDER BY all_sessions.country, all_sessions.city, TotalRevenue desc
)
select 
*,
RANK() OVER(ORDER BY TotalRevenue DESC) AS global_rank

FROM CTE
ORDER BY global_rank



Answer:

The UNITED STATES had the highest number of revenue generated as it has 15 states generating revenue more than other countries.

country	city	totalrevenue	global_rank
United States	Mountain View	10470949996	1
United States	San Bruno	4230990000	2
United States	New York	3124275708	3
United States	Sunnyvale	2999357772	4
United States	Chicago	1383630000	5
United States	Kirkland	1103520000	6
United States	San Francisco	954103332	7
United States	Jersey City	933850000	8
United States	Charlotte	932885550	9
United States	Los Angeles	926009999	10
United States	Seattle	732825713	11
United States	Palo Alto	709000000	12
United States	Austin	643689998	13
United States	Milpitas	494300000	14
Canada	Toronto	447480000	15
United States	Ann Arbor	355879999	16
United States	Salem	246430000	17
United States	San Jose	236350000	18
United States	Cambridge	147430000	19
United States	Fremont	124000000	20
United States	Atlanta	83000000	21
United States	South San Francisco	82420000	22
United States	Denver	41980000	23
Japan	Yokohama	30880000	24
Switzerland	Zurich	16990000	25







