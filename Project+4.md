

```python
#Import file
import pandas as pd
```


```python
#Read file and path
fname = "purchase_data.json"
pdata = pd.read_json(fname)

#view Pdata
pdata.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>



PLAYER COUNT

#Total Number of Players


```python
#Finding player count unique name & length list
pcount = len(pdata['SN'].unique())

#DataFrame for player count and total
player_df = pd.DataFrame([{'Total player': pcount}])

player_df.set_index('Total player', inplace = True)
player_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
    </tr>
    <tr>
      <th>Total player</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>573</th>
    </tr>
  </tbody>
</table>
</div>



PURCHASING ANALYSIS(TOTAL)

#Number of Unique Items
#Average Purchase Price
#Total Number of Purchases
#Total Revenue


```python
#Data inspection
pdata['Item ID'].value_counts()
```




    84     11
    39     11
    31      9
    34      9
    175     9
    13      9
    106     8
    44      8
    92      8
    65      8
    152     8
    107     8
    172     7
    179     7
    115     7
    154     7
    79      7
    158     7
    108     7
    66      7
    11      7
    130     7
    18      7
    124     6
    103     6
    101     6
    121     6
    102     6
    73      6
    145     6
           ..
    116     2
    89      2
    64      2
    9       2
    167     2
    80      2
    74      2
    72      2
    146     2
    149     2
    150     2
    178     2
    62      2
    58      2
    56      2
    55      2
    4       1
    2       1
    3       1
    59      1
    28      1
    168     1
    164     1
    43      1
    156     1
    147     1
    136     1
    126     1
    109     1
    0       1
    Name: Item ID, Length: 183, dtype: int64




```python
#for unique items
unique_items = pd.DataFrame(pdata['Item ID'].unique())
len(unique_items)
```




    183




```python
#DataFrame for last Item ID occurence
duplicate_items = pdata.drop_duplicates(['Item ID'], keep = 'last')
duplicate_items
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>21</th>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
    </tr>
    <tr>
      <th>59</th>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
    </tr>
    <tr>
      <th>63</th>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
    </tr>
    <tr>
      <th>88</th>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
    </tr>
    <tr>
      <th>129</th>
      <td>23</td>
      <td>Female</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>3.25</td>
      <td>Eurinu48</td>
    </tr>
    <tr>
      <th>173</th>
      <td>30</td>
      <td>Male</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
    </tr>
    <tr>
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
    </tr>
    <tr>
      <th>185</th>
      <td>22</td>
      <td>Male</td>
      <td>167</td>
      <td>Malice, Legacy of the Queen</td>
      <td>2.38</td>
      <td>Siarinum43</td>
    </tr>
    <tr>
      <th>196</th>
      <td>20</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>1.50</td>
      <td>Chanirra56</td>
    </tr>
    <tr>
      <th>205</th>
      <td>17</td>
      <td>Male</td>
      <td>147</td>
      <td>Hellreaver, Heirloom of Inception</td>
      <td>3.59</td>
      <td>Airidil41</td>
    </tr>
    <tr>
      <th>239</th>
      <td>24</td>
      <td>Female</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>3.03</td>
      <td>Ethruard50</td>
    </tr>
    <tr>
      <th>253</th>
      <td>15</td>
      <td>Male</td>
      <td>149</td>
      <td>Tranquility, Razor of Black Magic</td>
      <td>2.47</td>
      <td>Meosridil82</td>
    </tr>
    <tr>
      <th>256</th>
      <td>22</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>3.47</td>
      <td>Iadueria43</td>
    </tr>
    <tr>
      <th>300</th>
      <td>15</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Lisossan98</td>
    </tr>
    <tr>
      <th>315</th>
      <td>24</td>
      <td>Male</td>
      <td>54</td>
      <td>Eternal Cleaver</td>
      <td>3.14</td>
      <td>Aelin32</td>
    </tr>
    <tr>
      <th>336</th>
      <td>15</td>
      <td>Male</td>
      <td>173</td>
      <td>Stormfury Longsword</td>
      <td>4.83</td>
      <td>Iskadarya95</td>
    </tr>
    <tr>
      <th>341</th>
      <td>20</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>2.04</td>
      <td>Aeliriarin93</td>
    </tr>
    <tr>
      <th>342</th>
      <td>15</td>
      <td>Female</td>
      <td>50</td>
      <td>Dawn</td>
      <td>2.55</td>
      <td>Raedalis34</td>
    </tr>
    <tr>
      <th>387</th>
      <td>24</td>
      <td>Female</td>
      <td>51</td>
      <td>Endbringer</td>
      <td>2.67</td>
      <td>Ethruard50</td>
    </tr>
    <tr>
      <th>398</th>
      <td>25</td>
      <td>Female</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>4.77</td>
      <td>Tyaelistidru84</td>
    </tr>
    <tr>
      <th>401</th>
      <td>17</td>
      <td>Male</td>
      <td>121</td>
      <td>Massacre</td>
      <td>3.42</td>
      <td>Leulaesti78</td>
    </tr>
    <tr>
      <th>411</th>
      <td>25</td>
      <td>Male</td>
      <td>7</td>
      <td>Thorn, Satchel of Dark Souls</td>
      <td>4.51</td>
      <td>Saedue76</td>
    </tr>
    <tr>
      <th>419</th>
      <td>25</td>
      <td>Female</td>
      <td>42</td>
      <td>The Decapitator</td>
      <td>4.82</td>
      <td>Tyeuladeu30</td>
    </tr>
    <tr>
      <th>421</th>
      <td>22</td>
      <td>Male</td>
      <td>150</td>
      <td>Deathraze</td>
      <td>4.54</td>
      <td>Ina92</td>
    </tr>
    <tr>
      <th>422</th>
      <td>24</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.92</td>
      <td>Saida58</td>
    </tr>
    <tr>
      <th>423</th>
      <td>32</td>
      <td>Other / Non-Disclosed</td>
      <td>29</td>
      <td>Chaos, Ender of the End</td>
      <td>3.79</td>
      <td>Aithelis62</td>
    </tr>
    <tr>
      <th>430</th>
      <td>27</td>
      <td>Male</td>
      <td>74</td>
      <td>Yearning Crusher</td>
      <td>1.06</td>
      <td>Lirtassa47</td>
    </tr>
    <tr>
      <th>436</th>
      <td>10</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>4.82</td>
      <td>Ethrusuard41</td>
    </tr>
    <tr>
      <th>446</th>
      <td>22</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>Lisosianya62</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>746</th>
      <td>35</td>
      <td>Male</td>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>Ralasti48</td>
    </tr>
    <tr>
      <th>748</th>
      <td>15</td>
      <td>Male</td>
      <td>120</td>
      <td>Agatha</td>
      <td>1.91</td>
      <td>Isri49</td>
    </tr>
    <tr>
      <th>749</th>
      <td>21</td>
      <td>Male</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>1.79</td>
      <td>Frichassala85</td>
    </tr>
    <tr>
      <th>750</th>
      <td>23</td>
      <td>Male</td>
      <td>86</td>
      <td>Stormfury Lantern</td>
      <td>1.28</td>
      <td>Eollym91</td>
    </tr>
    <tr>
      <th>752</th>
      <td>15</td>
      <td>Female</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>2.37</td>
      <td>Yalostiphos68</td>
    </tr>
    <tr>
      <th>753</th>
      <td>20</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>Thryallym62</td>
    </tr>
    <tr>
      <th>755</th>
      <td>22</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Ailaesuir66</td>
    </tr>
    <tr>
      <th>756</th>
      <td>22</td>
      <td>Male</td>
      <td>6</td>
      <td>Rusty Skull</td>
      <td>1.20</td>
      <td>Siasri67</td>
    </tr>
    <tr>
      <th>757</th>
      <td>35</td>
      <td>Male</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Seosri62</td>
    </tr>
    <tr>
      <th>759</th>
      <td>19</td>
      <td>Male</td>
      <td>87</td>
      <td>Deluge, Edge of the West</td>
      <td>2.20</td>
      <td>Chanirrasta87</td>
    </tr>
    <tr>
      <th>760</th>
      <td>29</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>761</th>
      <td>28</td>
      <td>Male</td>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>Raeduerin33</td>
    </tr>
    <tr>
      <th>762</th>
      <td>36</td>
      <td>Male</td>
      <td>52</td>
      <td>Hatred</td>
      <td>4.39</td>
      <td>Lisosiast26</td>
    </tr>
    <tr>
      <th>763</th>
      <td>27</td>
      <td>Other / Non-Disclosed</td>
      <td>48</td>
      <td>Rage, Legacy of the Lone Victor</td>
      <td>4.32</td>
      <td>Eurisuru25</td>
    </tr>
    <tr>
      <th>764</th>
      <td>25</td>
      <td>Male</td>
      <td>70</td>
      <td>Hope's End</td>
      <td>3.89</td>
      <td>Assassasda84</td>
    </tr>
    <tr>
      <th>765</th>
      <td>15</td>
      <td>Male</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aerithnucal56</td>
    </tr>
    <tr>
      <th>766</th>
      <td>22</td>
      <td>Female</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>Nitherian58</td>
    </tr>
    <tr>
      <th>767</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Hailaphos89</td>
    </tr>
    <tr>
      <th>768</th>
      <td>21</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>3.56</td>
      <td>Chamucosda93</td>
    </tr>
    <tr>
      <th>769</th>
      <td>24</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>3.74</td>
      <td>Frichilsasya78</td>
    </tr>
    <tr>
      <th>770</th>
      <td>22</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.27</td>
      <td>Aenasu69</td>
    </tr>
    <tr>
      <th>771</th>
      <td>24</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>1.03</td>
      <td>Lassista97</td>
    </tr>
    <tr>
      <th>772</th>
      <td>15</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Sidap51</td>
    </tr>
    <tr>
      <th>773</th>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Chamadarsda63</td>
    </tr>
    <tr>
      <th>774</th>
      <td>24</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Lassassast73</td>
    </tr>
    <tr>
      <th>775</th>
      <td>22</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>3.62</td>
      <td>Eural50</td>
    </tr>
    <tr>
      <th>776</th>
      <td>14</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Lirtossa78</td>
    </tr>
    <tr>
      <th>777</th>
      <td>20</td>
      <td>Male</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.15</td>
      <td>Tillyrin30</td>
    </tr>
    <tr>
      <th>778</th>
      <td>20</td>
      <td>Male</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>1.72</td>
      <td>Quelaton80</td>
    </tr>
    <tr>
      <th>779</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>Alim85</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 6 columns</p>
</div>




```python
# Unique ID counts
totalunique = len(duplicate_items)
totalunique
```




    183




```python
#Total purchases by price occurence
totalpurch = pdata['Price'].count()
totalpurch
```




    780




```python
#Total revenue by summing price occurrence
totalrev = round(pdata['Price'].sum(),2)
totalrev
```




    2286.33




```python
#Total average
avgprice = round(totalrev/totalpurch, 2)
avgprice
```




    2.9300000000000002




```python
#Analysis DataFrame
purchase_analysis = pd.DataFrame([{"Number of Unique Items": totalunique, "Average Purchase Price": avgprice, "Total Purchases": totalpurch, "Total Revenue": totalrev}])
purchase_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.93</td>
      <td>183</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>



GENDER DEMOGRAPHICS
#Percentage and Count of Male Players
#Percentage and Count of Female Players
#Percentage and Count of Other / Non-Disclosed


```python
#Unique Player name
duplicate_players = pdata.drop_duplicates(['SN'], keep ='last')
duplicate_players
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
    </tr>
    <tr>
      <th>11</th>
      <td>20</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>Sally64</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>19</th>
      <td>31</td>
      <td>Male</td>
      <td>177</td>
      <td>Winterthorn, Defender of Shifting Worlds</td>
      <td>4.89</td>
      <td>Assossa43</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24</td>
      <td>Male</td>
      <td>78</td>
      <td>Glimmer, Ender of the Moon</td>
      <td>2.33</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>23</th>
      <td>19</td>
      <td>Male</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Chanosia65</td>
    </tr>
    <tr>
      <th>27</th>
      <td>34</td>
      <td>Male</td>
      <td>106</td>
      <td>Crying Steel Sickle</td>
      <td>2.29</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>28</th>
      <td>15</td>
      <td>Male</td>
      <td>49</td>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>4.23</td>
      <td>Ilariarin45</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
    <tr>
      <th>30</th>
      <td>21</td>
      <td>Female</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Eulaeria40</td>
    </tr>
    <tr>
      <th>31</th>
      <td>18</td>
      <td>Male</td>
      <td>37</td>
      <td>Shadow Strike, Glory of Ending Hope</td>
      <td>1.93</td>
      <td>Iarilis73</td>
    </tr>
    <tr>
      <th>34</th>
      <td>22</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>Yararmol43</td>
    </tr>
    <tr>
      <th>35</th>
      <td>21</td>
      <td>Female</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aisur51</td>
    </tr>
    <tr>
      <th>36</th>
      <td>20</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Undare39</td>
    </tr>
    <tr>
      <th>37</th>
      <td>31</td>
      <td>Male</td>
      <td>171</td>
      <td>Scalpel</td>
      <td>3.62</td>
      <td>Sondossa91</td>
    </tr>
    <tr>
      <th>39</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Lassilsa63</td>
    </tr>
    <tr>
      <th>40</th>
      <td>32</td>
      <td>Male</td>
      <td>7</td>
      <td>Thorn, Satchel of Dark Souls</td>
      <td>4.51</td>
      <td>Tyisur83</td>
    </tr>
    <tr>
      <th>41</th>
      <td>19</td>
      <td>Female</td>
      <td>124</td>
      <td>Venom Claymore</td>
      <td>2.72</td>
      <td>Aeral43</td>
    </tr>
    <tr>
      <th>42</th>
      <td>24</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>1.03</td>
      <td>Lassadarsda57</td>
    </tr>
    <tr>
      <th>44</th>
      <td>22</td>
      <td>Male</td>
      <td>85</td>
      <td>Malificent Bag</td>
      <td>2.17</td>
      <td>Frichjask31</td>
    </tr>
    <tr>
      <th>46</th>
      <td>11</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>3.47</td>
      <td>Palatyon26</td>
    </tr>
    <tr>
      <th>54</th>
      <td>25</td>
      <td>Female</td>
      <td>101</td>
      <td>Final Critic</td>
      <td>4.62</td>
      <td>Minduli80</td>
    </tr>
    <tr>
      <th>55</th>
      <td>24</td>
      <td>Male</td>
      <td>140</td>
      <td>Striker</td>
      <td>3.82</td>
      <td>Heunadil74</td>
    </tr>
    <tr>
      <th>56</th>
      <td>23</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Marilsasya33</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>750</th>
      <td>23</td>
      <td>Male</td>
      <td>86</td>
      <td>Stormfury Lantern</td>
      <td>1.28</td>
      <td>Eollym91</td>
    </tr>
    <tr>
      <th>751</th>
      <td>26</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Lisjasksda68</td>
    </tr>
    <tr>
      <th>752</th>
      <td>15</td>
      <td>Female</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>2.37</td>
      <td>Yalostiphos68</td>
    </tr>
    <tr>
      <th>753</th>
      <td>20</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>Thryallym62</td>
    </tr>
    <tr>
      <th>754</th>
      <td>31</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Sondastan54</td>
    </tr>
    <tr>
      <th>755</th>
      <td>22</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Ailaesuir66</td>
    </tr>
    <tr>
      <th>756</th>
      <td>22</td>
      <td>Male</td>
      <td>6</td>
      <td>Rusty Skull</td>
      <td>1.20</td>
      <td>Siasri67</td>
    </tr>
    <tr>
      <th>757</th>
      <td>35</td>
      <td>Male</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Seosri62</td>
    </tr>
    <tr>
      <th>758</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Ryastycal90</td>
    </tr>
    <tr>
      <th>759</th>
      <td>19</td>
      <td>Male</td>
      <td>87</td>
      <td>Deluge, Edge of the West</td>
      <td>2.20</td>
      <td>Chanirrasta87</td>
    </tr>
    <tr>
      <th>760</th>
      <td>29</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>761</th>
      <td>28</td>
      <td>Male</td>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>Raeduerin33</td>
    </tr>
    <tr>
      <th>762</th>
      <td>36</td>
      <td>Male</td>
      <td>52</td>
      <td>Hatred</td>
      <td>4.39</td>
      <td>Lisosiast26</td>
    </tr>
    <tr>
      <th>763</th>
      <td>27</td>
      <td>Other / Non-Disclosed</td>
      <td>48</td>
      <td>Rage, Legacy of the Lone Victor</td>
      <td>4.32</td>
      <td>Eurisuru25</td>
    </tr>
    <tr>
      <th>764</th>
      <td>25</td>
      <td>Male</td>
      <td>70</td>
      <td>Hope's End</td>
      <td>3.89</td>
      <td>Assassasda84</td>
    </tr>
    <tr>
      <th>765</th>
      <td>15</td>
      <td>Male</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aerithnucal56</td>
    </tr>
    <tr>
      <th>766</th>
      <td>22</td>
      <td>Female</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>Nitherian58</td>
    </tr>
    <tr>
      <th>767</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Hailaphos89</td>
    </tr>
    <tr>
      <th>768</th>
      <td>21</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>3.56</td>
      <td>Chamucosda93</td>
    </tr>
    <tr>
      <th>769</th>
      <td>24</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>3.74</td>
      <td>Frichilsasya78</td>
    </tr>
    <tr>
      <th>770</th>
      <td>22</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.27</td>
      <td>Aenasu69</td>
    </tr>
    <tr>
      <th>771</th>
      <td>24</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>1.03</td>
      <td>Lassista97</td>
    </tr>
    <tr>
      <th>772</th>
      <td>15</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Sidap51</td>
    </tr>
    <tr>
      <th>773</th>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Chamadarsda63</td>
    </tr>
    <tr>
      <th>774</th>
      <td>24</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Lassassast73</td>
    </tr>
    <tr>
      <th>775</th>
      <td>22</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>3.62</td>
      <td>Eural50</td>
    </tr>
    <tr>
      <th>776</th>
      <td>14</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Lirtossa78</td>
    </tr>
    <tr>
      <th>777</th>
      <td>20</td>
      <td>Male</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.15</td>
      <td>Tillyrin30</td>
    </tr>
    <tr>
      <th>778</th>
      <td>20</td>
      <td>Male</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>1.72</td>
      <td>Quelaton80</td>
    </tr>
    <tr>
      <th>779</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>Alim85</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 6 columns</p>
</div>




```python
#Gender values
gcount = duplicate_players["Gender"].value_counts().reset_index()
gcount
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>465</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Adding columns for player % and Gender
gcount["% of players"] = gcount["Gender"]/pcount * 100

#Renaming Columns
gcount.rename(columns = {"index": "Gender", "Gender": "# of Players"}, inplace = True)
gcount
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th># of Players</th>
      <th>% of players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>465</td>
      <td>81.151832</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>100</td>
      <td>17.452007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>8</td>
      <td>1.396161</td>
    </tr>
  </tbody>
</table>
</div>



PURCHASE ANALYSIS GENDER
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Normalized Totals



```python
#Purchase count by gender
pcountgen = pd.DataFrame(pdata.groupby("Gender")["Gender"].count())
pcountgen
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender sum price
totalpgen = pd.DataFrame(pdata.groupby("Gender")["Price"].sum())
totalpgen
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merging two data frames
p_analysis = pd.merge(pcountgen, totalpgen, left_index = True, right_index = True)
p_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Renaming columns
p_analysis.rename(columns = {"Gender": "No of Purchases", "Price": "Total Purchase Value"}, inplace=True)
p_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>No of Purchases</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Adding column average price by gender dividing total purchase No. of purchase
p_analysis['Average Purchase Price'] = p_analysis['Total Purchase Value']/p_analysis['No of Purchases']
p_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>No of Purchases</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>382.91</td>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>1867.68</td>
      <td>2.950521</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>35.74</td>
      <td>3.249091</td>
    </tr>
  </tbody>
</table>
</div>




```python
p_analysis = p_analysis.merge(gcount, left_index = True, right_index = True)
p_analysis["Normalized Totals"] = p_analysis["Total Purchase Value"]/p_analysis["% of players"]
p_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>No of Purchases</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
      <th>Gender_x</th>
      <th># of Players_x</th>
      <th>% of players_x</th>
      <th>Normalized Totals</th>
      <th>Gender_y</th>
      <th># of Players_y</th>
      <th>% of players_y</th>
      <th>Gender</th>
      <th># of Players</th>
      <th>% of players</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
clean = p_analysis.rename(columns={"Gender_x":"Gender","# of Players_x":"# of Players","% of players_x":"% of players","Gender_y":"Gender","# of Players_y":"# of Players","% of players_y":"% of players"})
clean
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>No of Purchases</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
      <th>Gender</th>
      <th># of Players</th>
      <th>% of players</th>
      <th>Normalized Totals</th>
      <th>Gender</th>
      <th># of Players</th>
      <th>% of players</th>
      <th>Gender</th>
      <th># of Players</th>
      <th>% of players</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
#deleting unneeded columns
del p_analysis["% of players"]
del p_analysis["# of Players"]
p_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>No of Purchases</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
      <th>Gender_x</th>
      <th># of Players_x</th>
      <th>% of players_x</th>
      <th>Normalized Totals</th>
      <th>Gender_y</th>
      <th># of Players_y</th>
      <th>% of players_y</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



AGE DEMOGRAPGICS
#The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Normalized Totals


```python
#Age_bin column based on age range
pdata.loc[(pdata['Age'] < 10), 'age_bin'] = "< 10"
pdata.loc[(pdata['Age'] >= 10) & (pdata['Age'] <= 14), 'age_bin'] = "10 - 14"
pdata.loc[(pdata['Age'] >= 15) & (pdata['Age'] <= 19), 'age_bin'] = "15 - 19"
pdata.loc[(pdata['Age'] >= 20) & (pdata['Age'] <= 24), 'age_bin'] = "20 - 24"
pdata.loc[(pdata['Age'] >= 25) & (pdata['Age'] <= 29), 'age_bin'] = "25 - 29"
pdata.loc[(pdata['Age'] >= 30) & (pdata['Age'] <= 34), 'age_bin'] = "30 - 34"
pdata.loc[(pdata['Age'] >= 35) & (pdata['Age'] <= 39), 'age_bin'] = "35 - 39"
pdata.loc[(pdata['Age'] >= 40), 'age_bin'] = "> 40"
pdata
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>age_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Hilaerin92</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>10</th>
      <td>24</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>3.81</td>
      <td>Chamosia29</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>11</th>
      <td>20</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>Sally64</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>12</th>
      <td>30</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>Iskossa88</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>13</th>
      <td>23</td>
      <td>Male</td>
      <td>77</td>
      <td>Piety, Guardian of Riddles</td>
      <td>3.68</td>
      <td>Seorithstilis90</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>14</th>
      <td>40</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Sundast29</td>
      <td>&gt; 40</td>
    </tr>
    <tr>
      <th>15</th>
      <td>21</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>4.77</td>
      <td>Haellysu29</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>18</th>
      <td>28</td>
      <td>Male</td>
      <td>91</td>
      <td>Celeste</td>
      <td>3.71</td>
      <td>Iskista88</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>19</th>
      <td>31</td>
      <td>Male</td>
      <td>177</td>
      <td>Winterthorn, Defender of Shifting Worlds</td>
      <td>4.89</td>
      <td>Assossa43</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24</td>
      <td>Male</td>
      <td>78</td>
      <td>Glimmer, Ender of the Moon</td>
      <td>2.33</td>
      <td>Irith83</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
      <td>10 - 14</td>
    </tr>
    <tr>
      <th>23</th>
      <td>19</td>
      <td>Male</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Chanosia65</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>24</th>
      <td>11</td>
      <td>Male</td>
      <td>65</td>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>Qarwen67</td>
      <td>10 - 14</td>
    </tr>
    <tr>
      <th>25</th>
      <td>21</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Idai61</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>26</th>
      <td>29</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Aerithllora36</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>27</th>
      <td>34</td>
      <td>Male</td>
      <td>106</td>
      <td>Crying Steel Sickle</td>
      <td>2.29</td>
      <td>Assastnya25</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>28</th>
      <td>15</td>
      <td>Male</td>
      <td>49</td>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>4.23</td>
      <td>Ilariarin45</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>750</th>
      <td>23</td>
      <td>Male</td>
      <td>86</td>
      <td>Stormfury Lantern</td>
      <td>1.28</td>
      <td>Eollym91</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>751</th>
      <td>26</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Lisjasksda68</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>752</th>
      <td>15</td>
      <td>Female</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>2.37</td>
      <td>Yalostiphos68</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>753</th>
      <td>20</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>Thryallym62</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>754</th>
      <td>31</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Sondastan54</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>755</th>
      <td>22</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Ailaesuir66</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>756</th>
      <td>22</td>
      <td>Male</td>
      <td>6</td>
      <td>Rusty Skull</td>
      <td>1.20</td>
      <td>Siasri67</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>757</th>
      <td>35</td>
      <td>Male</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Seosri62</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>758</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Ryastycal90</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>759</th>
      <td>19</td>
      <td>Male</td>
      <td>87</td>
      <td>Deluge, Edge of the West</td>
      <td>2.20</td>
      <td>Chanirrasta87</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>760</th>
      <td>29</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>Aerithllora36</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>761</th>
      <td>28</td>
      <td>Male</td>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>Raeduerin33</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>762</th>
      <td>36</td>
      <td>Male</td>
      <td>52</td>
      <td>Hatred</td>
      <td>4.39</td>
      <td>Lisosiast26</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>763</th>
      <td>27</td>
      <td>Other / Non-Disclosed</td>
      <td>48</td>
      <td>Rage, Legacy of the Lone Victor</td>
      <td>4.32</td>
      <td>Eurisuru25</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>764</th>
      <td>25</td>
      <td>Male</td>
      <td>70</td>
      <td>Hope's End</td>
      <td>3.89</td>
      <td>Assassasda84</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>765</th>
      <td>15</td>
      <td>Male</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aerithnucal56</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>766</th>
      <td>22</td>
      <td>Female</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>Nitherian58</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>767</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Hailaphos89</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>768</th>
      <td>21</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>3.56</td>
      <td>Chamucosda93</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>769</th>
      <td>24</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>3.74</td>
      <td>Frichilsasya78</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>770</th>
      <td>22</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.27</td>
      <td>Aenasu69</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>771</th>
      <td>24</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>1.03</td>
      <td>Lassista97</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>772</th>
      <td>15</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Sidap51</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>773</th>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Chamadarsda63</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>774</th>
      <td>24</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Lassassast73</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>775</th>
      <td>22</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>3.62</td>
      <td>Eural50</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>776</th>
      <td>14</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Lirtossa78</td>
      <td>10 - 14</td>
    </tr>
    <tr>
      <th>777</th>
      <td>20</td>
      <td>Male</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.15</td>
      <td>Tillyrin30</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>778</th>
      <td>20</td>
      <td>Male</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>1.72</td>
      <td>Quelaton80</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>779</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>Alim85</td>
      <td>20 - 24</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 7 columns</p>
</div>




```python
#count purchase by age_bin
pcountage = pd.DataFrame(pdata.groupby('age_bin')['SN'].count())
pcountage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>35</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>133</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>336</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>125</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>64</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>42</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>28</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
#average price of purchase age_bin
avgpriceage = pd.DataFrame(pdata.groupby('age_bin')['Price'].mean())
avgpriceage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>2.905414</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>2.913006</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>2.962640</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>3.082031</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>2.842857</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>2.980714</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>3.161765</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total purchase value age_bin
totalpage = pd.DataFrame(pdata.groupby("age_bin")["Price"].mean())
totalpage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>2.905414</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>2.913006</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>2.962640</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>3.082031</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>2.842857</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>2.980714</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>3.161765</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Drop multiple SN and keep last and count unique player by age_bin
ddage = pd.DataFrame(pdata.drop_duplicates('SN', keep = 'last').groupby('age_bin')['SN'].count())
ddage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>23</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>100</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>259</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>87</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>47</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>27</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>19</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merging into one dataframe
mergeage = pd.merge(pcountage, avgpriceage, left_index = True, right_index = True).merge(totalpage, left_index = True, right_index = True).merge(ddage, left_index = True, right_index = True)
mergeage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN_x</th>
      <th>Price_x</th>
      <th>Price_y</th>
      <th>SN_y</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>35</td>
      <td>2.770000</td>
      <td>2.770000</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>133</td>
      <td>2.905414</td>
      <td>2.905414</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>336</td>
      <td>2.913006</td>
      <td>2.913006</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>125</td>
      <td>2.962640</td>
      <td>2.962640</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>64</td>
      <td>3.082031</td>
      <td>3.082031</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>42</td>
      <td>2.842857</td>
      <td>2.842857</td>
      <td>27</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>28</td>
      <td>2.980714</td>
      <td>2.980714</td>
      <td>19</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>17</td>
      <td>3.161765</td>
      <td>3.161765</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Rename columns
mergeage.rename(columns = {"SN_x": "# of Purchases", "Price_x": "Average Purchase Price", "Price_y": "Total Purchase Value", "SN_y": "# of Purchasers"}, inplace = True)
mergeage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th># of Purchases</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th># of Purchasers</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>35</td>
      <td>2.770000</td>
      <td>2.770000</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>133</td>
      <td>2.905414</td>
      <td>2.905414</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>336</td>
      <td>2.913006</td>
      <td>2.913006</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>125</td>
      <td>2.962640</td>
      <td>2.962640</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>64</td>
      <td>3.082031</td>
      <td>3.082031</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>42</td>
      <td>2.842857</td>
      <td>2.842857</td>
      <td>27</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>28</td>
      <td>2.980714</td>
      <td>2.980714</td>
      <td>19</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>17</td>
      <td>3.161765</td>
      <td>3.161765</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Normalized totals
mergeage['Normalized Totals'] = mergeage['Total Purchase Value']/mergeage['# of Purchasers']
mergeage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th># of Purchases</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th># of Purchasers</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>age_bin</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>35</td>
      <td>2.770000</td>
      <td>2.770000</td>
      <td>23</td>
      <td>0.120435</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>133</td>
      <td>2.905414</td>
      <td>2.905414</td>
      <td>100</td>
      <td>0.029054</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>336</td>
      <td>2.913006</td>
      <td>2.913006</td>
      <td>259</td>
      <td>0.011247</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>125</td>
      <td>2.962640</td>
      <td>2.962640</td>
      <td>87</td>
      <td>0.034053</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>64</td>
      <td>3.082031</td>
      <td>3.082031</td>
      <td>47</td>
      <td>0.065575</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>42</td>
      <td>2.842857</td>
      <td>2.842857</td>
      <td>27</td>
      <td>0.105291</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>28</td>
      <td>2.980714</td>
      <td>2.980714</td>
      <td>19</td>
      <td>0.156880</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>17</td>
      <td>3.161765</td>
      <td>3.161765</td>
      <td>11</td>
      <td>0.287433</td>
    </tr>
  </tbody>
</table>
</div>




```python
#rest index for aesthetics
mergeage.index.rename("Age", inplace = True)
mergeage
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th># of Purchases</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th># of Purchasers</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 - 14</th>
      <td>35</td>
      <td>2.770000</td>
      <td>2.770000</td>
      <td>23</td>
      <td>0.120435</td>
    </tr>
    <tr>
      <th>15 - 19</th>
      <td>133</td>
      <td>2.905414</td>
      <td>2.905414</td>
      <td>100</td>
      <td>0.029054</td>
    </tr>
    <tr>
      <th>20 - 24</th>
      <td>336</td>
      <td>2.913006</td>
      <td>2.913006</td>
      <td>259</td>
      <td>0.011247</td>
    </tr>
    <tr>
      <th>25 - 29</th>
      <td>125</td>
      <td>2.962640</td>
      <td>2.962640</td>
      <td>87</td>
      <td>0.034053</td>
    </tr>
    <tr>
      <th>30 - 34</th>
      <td>64</td>
      <td>3.082031</td>
      <td>3.082031</td>
      <td>47</td>
      <td>0.065575</td>
    </tr>
    <tr>
      <th>35 - 39</th>
      <td>42</td>
      <td>2.842857</td>
      <td>2.842857</td>
      <td>27</td>
      <td>0.105291</td>
    </tr>
    <tr>
      <th>&lt; 10</th>
      <td>28</td>
      <td>2.980714</td>
      <td>2.980714</td>
      <td>19</td>
      <td>0.156880</td>
    </tr>
    <tr>
      <th>&gt; 40</th>
      <td>17</td>
      <td>3.161765</td>
      <td>3.161765</td>
      <td>11</td>
      <td>0.287433</td>
    </tr>
  </tbody>
</table>
</div>



TOP SPENDERS
#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#SN
#Purchase Count
#Average Purchase Price
#Total Purchase Value


```python
pamount_by_SN = pd.DataFrame(pdata.groupby('SN')['Price'].sum())
pamount_by_SN
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>5.06</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.14</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>6.72</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.04</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>8.98</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.32</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.15</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.61</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.55</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.65</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.27</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.72</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.25</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.35</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>6.60</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.88</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>10.45</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>3.18</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.69</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.38</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.66</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.32</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.97</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>6.84</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.57</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.53</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.90</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.04</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.08</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.93</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>8.56</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>9.09</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.88</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.71</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.41</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.37</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>4.19</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.55</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.88</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.24</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.19</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.35</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>4.81</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.91</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>6.98</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>10.40</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.60</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.78</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.04</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.14</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>7.77</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.41</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.71</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 1 columns</p>
</div>




```python
nump_by_SN = pd.DataFrame(pdata.groupby('SN')['Price'].count())
nump_by_SN
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 1 columns</p>
</div>




```python
avgp_by_SN = pd.DataFrame(pdata.groupby('SN')['Price'].mean())
avgp_by_SN
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.270000</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>2.530000</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>3.360000</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>4.490000</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.320000</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.150000</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.610000</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.650000</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.270000</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.720000</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>3.300000</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>3.483333</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>1.590000</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.690000</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.380000</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.820000</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.660000</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.320000</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.970000</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>3.420000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.570000</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.530000</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.080000</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.930000</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>3.030000</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.710000</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.370000</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>2.095000</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.880000</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.240000</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.190000</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>2.405000</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>3.490000</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>3.466667</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.780000</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>3.885000</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>1.230000</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.710000</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 1 columns</p>
</div>




```python
#Merge
merged = pd.merge(pamount_by_SN, nump_by_SN, left_index = True, right_index = True).merge(avgp_by_SN, left_index=True, right_index=True)
merged
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price_x</th>
      <th>Price_y</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1</td>
      <td>1.270000</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>5.06</td>
      <td>2</td>
      <td>2.530000</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>6.72</td>
      <td>2</td>
      <td>3.360000</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>8.98</td>
      <td>2</td>
      <td>4.490000</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.32</td>
      <td>1</td>
      <td>4.320000</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.15</td>
      <td>1</td>
      <td>3.150000</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.61</td>
      <td>1</td>
      <td>3.610000</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.65</td>
      <td>1</td>
      <td>1.650000</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.27</td>
      <td>1</td>
      <td>3.270000</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.72</td>
      <td>1</td>
      <td>2.720000</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.25</td>
      <td>1</td>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>6.60</td>
      <td>2</td>
      <td>3.300000</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>10.45</td>
      <td>3</td>
      <td>3.483333</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>3.18</td>
      <td>2</td>
      <td>1.590000</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.69</td>
      <td>1</td>
      <td>1.690000</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.38</td>
      <td>1</td>
      <td>2.380000</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.82</td>
      <td>1</td>
      <td>1.820000</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.66</td>
      <td>1</td>
      <td>4.660000</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.32</td>
      <td>1</td>
      <td>2.320000</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.97</td>
      <td>1</td>
      <td>2.970000</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>6.84</td>
      <td>2</td>
      <td>3.420000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.57</td>
      <td>1</td>
      <td>4.570000</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.53</td>
      <td>1</td>
      <td>4.530000</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.90</td>
      <td>1</td>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.08</td>
      <td>1</td>
      <td>4.080000</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.93</td>
      <td>1</td>
      <td>1.930000</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>8.56</td>
      <td>2</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>9.09</td>
      <td>3</td>
      <td>3.030000</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.37</td>
      <td>1</td>
      <td>2.370000</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>4.19</td>
      <td>2</td>
      <td>2.095000</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.88</td>
      <td>1</td>
      <td>2.880000</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.24</td>
      <td>1</td>
      <td>1.240000</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.19</td>
      <td>1</td>
      <td>2.190000</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>4.81</td>
      <td>2</td>
      <td>2.405000</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.91</td>
      <td>1</td>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>6.98</td>
      <td>2</td>
      <td>3.490000</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>10.40</td>
      <td>3</td>
      <td>3.466667</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.60</td>
      <td>1</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.78</td>
      <td>1</td>
      <td>2.780000</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>7.77</td>
      <td>2</td>
      <td>3.885000</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2.46</td>
      <td>2</td>
      <td>1.230000</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 3 columns</p>
</div>




```python
#Rename column
merged.rename(columns = {'Price_x': 'Total Purchase Value', 'Price_y':'Purchase Count', 'Price':'Average Purchase Price'}, inplace = True)
merged
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1</td>
      <td>1.270000</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>5.06</td>
      <td>2</td>
      <td>2.530000</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>6.72</td>
      <td>2</td>
      <td>3.360000</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>8.98</td>
      <td>2</td>
      <td>4.490000</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.32</td>
      <td>1</td>
      <td>4.320000</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.15</td>
      <td>1</td>
      <td>3.150000</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.61</td>
      <td>1</td>
      <td>3.610000</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.65</td>
      <td>1</td>
      <td>1.650000</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.27</td>
      <td>1</td>
      <td>3.270000</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.72</td>
      <td>1</td>
      <td>2.720000</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.25</td>
      <td>1</td>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>6.60</td>
      <td>2</td>
      <td>3.300000</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>10.45</td>
      <td>3</td>
      <td>3.483333</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>3.18</td>
      <td>2</td>
      <td>1.590000</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.69</td>
      <td>1</td>
      <td>1.690000</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.38</td>
      <td>1</td>
      <td>2.380000</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.82</td>
      <td>1</td>
      <td>1.820000</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.66</td>
      <td>1</td>
      <td>4.660000</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.32</td>
      <td>1</td>
      <td>2.320000</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.97</td>
      <td>1</td>
      <td>2.970000</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>6.84</td>
      <td>2</td>
      <td>3.420000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.57</td>
      <td>1</td>
      <td>4.570000</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.53</td>
      <td>1</td>
      <td>4.530000</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.90</td>
      <td>1</td>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.08</td>
      <td>1</td>
      <td>4.080000</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.93</td>
      <td>1</td>
      <td>1.930000</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>8.56</td>
      <td>2</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>9.09</td>
      <td>3</td>
      <td>3.030000</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.37</td>
      <td>1</td>
      <td>2.370000</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>4.19</td>
      <td>2</td>
      <td>2.095000</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.88</td>
      <td>1</td>
      <td>2.880000</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.24</td>
      <td>1</td>
      <td>1.240000</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.19</td>
      <td>1</td>
      <td>2.190000</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>4.81</td>
      <td>2</td>
      <td>2.405000</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.91</td>
      <td>1</td>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>6.98</td>
      <td>2</td>
      <td>3.490000</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>10.40</td>
      <td>3</td>
      <td>3.466667</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.60</td>
      <td>1</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.78</td>
      <td>1</td>
      <td>2.780000</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>7.77</td>
      <td>2</td>
      <td>3.885000</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2.46</td>
      <td>2</td>
      <td>1.230000</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 3 columns</p>
</div>




```python
#sort from highest to lowest
merged.sort_values('Total Purchase Value', ascending = False, inplace=True)
merged.head()
```

    /Users/sundayjoseph/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>17.06</td>
      <td>5</td>
      <td>3.412000</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>4</td>
      <td>3.390000</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>4</td>
      <td>3.185000</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>3</td>
      <td>4.243333</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3</td>
      <td>3.860000</td>
    </tr>
  </tbody>
</table>
</div>



MOST POPULAR ITEM
#Identify the 5 most popular items by purchase count, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value


```python
#Item count by ID
itemID = pd.DataFrame(pdata.groupby('Item ID')['Item ID'].count())
itemID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4</td>
    </tr>
    <tr>
      <th>17</th>
      <td>3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <td>4</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
    </tr>
    <tr>
      <th>22</th>
      <td>6</td>
    </tr>
    <tr>
      <th>23</th>
      <td>4</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>4</td>
    </tr>
    <tr>
      <th>26</th>
      <td>4</td>
    </tr>
    <tr>
      <th>27</th>
      <td>4</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>154</th>
      <td>7</td>
    </tr>
    <tr>
      <th>155</th>
      <td>3</td>
    </tr>
    <tr>
      <th>156</th>
      <td>1</td>
    </tr>
    <tr>
      <th>157</th>
      <td>4</td>
    </tr>
    <tr>
      <th>158</th>
      <td>7</td>
    </tr>
    <tr>
      <th>159</th>
      <td>5</td>
    </tr>
    <tr>
      <th>160</th>
      <td>5</td>
    </tr>
    <tr>
      <th>161</th>
      <td>5</td>
    </tr>
    <tr>
      <th>162</th>
      <td>3</td>
    </tr>
    <tr>
      <th>163</th>
      <td>3</td>
    </tr>
    <tr>
      <th>164</th>
      <td>1</td>
    </tr>
    <tr>
      <th>165</th>
      <td>3</td>
    </tr>
    <tr>
      <th>166</th>
      <td>3</td>
    </tr>
    <tr>
      <th>167</th>
      <td>2</td>
    </tr>
    <tr>
      <th>168</th>
      <td>1</td>
    </tr>
    <tr>
      <th>169</th>
      <td>4</td>
    </tr>
    <tr>
      <th>170</th>
      <td>5</td>
    </tr>
    <tr>
      <th>171</th>
      <td>5</td>
    </tr>
    <tr>
      <th>172</th>
      <td>7</td>
    </tr>
    <tr>
      <th>173</th>
      <td>5</td>
    </tr>
    <tr>
      <th>174</th>
      <td>5</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
    </tr>
    <tr>
      <th>176</th>
      <td>4</td>
    </tr>
    <tr>
      <th>177</th>
      <td>4</td>
    </tr>
    <tr>
      <th>178</th>
      <td>2</td>
    </tr>
    <tr>
      <th>179</th>
      <td>7</td>
    </tr>
    <tr>
      <th>180</th>
      <td>5</td>
    </tr>
    <tr>
      <th>181</th>
      <td>3</td>
    </tr>
    <tr>
      <th>182</th>
      <td>5</td>
    </tr>
    <tr>
      <th>183</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 1 columns</p>
</div>




```python
#Sorting from high to low
itemID.sort_values('Item ID', ascending = False, inplace = True)
itemID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>11</td>
    </tr>
    <tr>
      <th>84</th>
      <td>11</td>
    </tr>
    <tr>
      <th>31</th>
      <td>9</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
    </tr>
    <tr>
      <th>34</th>
      <td>9</td>
    </tr>
    <tr>
      <th>65</th>
      <td>8</td>
    </tr>
    <tr>
      <th>152</th>
      <td>8</td>
    </tr>
    <tr>
      <th>44</th>
      <td>8</td>
    </tr>
    <tr>
      <th>107</th>
      <td>8</td>
    </tr>
    <tr>
      <th>106</th>
      <td>8</td>
    </tr>
    <tr>
      <th>92</th>
      <td>8</td>
    </tr>
    <tr>
      <th>158</th>
      <td>7</td>
    </tr>
    <tr>
      <th>115</th>
      <td>7</td>
    </tr>
    <tr>
      <th>108</th>
      <td>7</td>
    </tr>
    <tr>
      <th>66</th>
      <td>7</td>
    </tr>
    <tr>
      <th>79</th>
      <td>7</td>
    </tr>
    <tr>
      <th>154</th>
      <td>7</td>
    </tr>
    <tr>
      <th>130</th>
      <td>7</td>
    </tr>
    <tr>
      <th>172</th>
      <td>7</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7</td>
    </tr>
    <tr>
      <th>179</th>
      <td>7</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7</td>
    </tr>
    <tr>
      <th>91</th>
      <td>6</td>
    </tr>
    <tr>
      <th>103</th>
      <td>6</td>
    </tr>
    <tr>
      <th>47</th>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
    </tr>
    <tr>
      <th>85</th>
      <td>6</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>116</th>
      <td>2</td>
    </tr>
    <tr>
      <th>96</th>
      <td>2</td>
    </tr>
    <tr>
      <th>178</th>
      <td>2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2</td>
    </tr>
    <tr>
      <th>55</th>
      <td>2</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2</td>
    </tr>
    <tr>
      <th>80</th>
      <td>2</td>
    </tr>
    <tr>
      <th>150</th>
      <td>2</td>
    </tr>
    <tr>
      <th>149</th>
      <td>2</td>
    </tr>
    <tr>
      <th>58</th>
      <td>2</td>
    </tr>
    <tr>
      <th>146</th>
      <td>2</td>
    </tr>
    <tr>
      <th>64</th>
      <td>2</td>
    </tr>
    <tr>
      <th>132</th>
      <td>2</td>
    </tr>
    <tr>
      <th>56</th>
      <td>2</td>
    </tr>
    <tr>
      <th>89</th>
      <td>2</td>
    </tr>
    <tr>
      <th>156</th>
      <td>1</td>
    </tr>
    <tr>
      <th>109</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>136</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
    <tr>
      <th>126</th>
      <td>1</td>
    </tr>
    <tr>
      <th>43</th>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1</td>
    </tr>
    <tr>
      <th>147</th>
      <td>1</td>
    </tr>
    <tr>
      <th>168</th>
      <td>1</td>
    </tr>
    <tr>
      <th>164</th>
      <td>1</td>
    </tr>
    <tr>
      <th>59</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 1 columns</p>
</div>




```python
#Keeping the first 6 rows
itemID = itemID.iloc[0:6][:]
itemID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>11</td>
    </tr>
    <tr>
      <th>84</th>
      <td>11</td>
    </tr>
    <tr>
      <th>31</th>
      <td>9</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
    </tr>
    <tr>
      <th>34</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Purchase value
itemtotal = pd.DataFrame(pdata.groupby('Item ID')['Price'].sum())
itemtotal
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.96</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.60</td>
    </tr>
    <tr>
      <th>7</th>
      <td>27.06</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23.46</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.08</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10.38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>17.64</td>
    </tr>
    <tr>
      <th>12</th>
      <td>21.50</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13.41</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7.95</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6.18</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12.44</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10.41</td>
    </tr>
    <tr>
      <th>18</th>
      <td>12.39</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7.96</td>
    </tr>
    <tr>
      <th>20</th>
      <td>5.92</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9.81</td>
    </tr>
    <tr>
      <th>22</th>
      <td>21.42</td>
    </tr>
    <tr>
      <th>23</th>
      <td>11.08</td>
    </tr>
    <tr>
      <th>24</th>
      <td>4.82</td>
    </tr>
    <tr>
      <th>25</th>
      <td>4.12</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7.52</td>
    </tr>
    <tr>
      <th>27</th>
      <td>15.84</td>
    </tr>
    <tr>
      <th>28</th>
      <td>3.04</td>
    </tr>
    <tr>
      <th>29</th>
      <td>11.37</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>154</th>
      <td>15.33</td>
    </tr>
    <tr>
      <th>155</th>
      <td>11.19</td>
    </tr>
    <tr>
      <th>156</th>
      <td>1.16</td>
    </tr>
    <tr>
      <th>157</th>
      <td>8.84</td>
    </tr>
    <tr>
      <th>158</th>
      <td>24.92</td>
    </tr>
    <tr>
      <th>159</th>
      <td>15.05</td>
    </tr>
    <tr>
      <th>160</th>
      <td>11.10</td>
    </tr>
    <tr>
      <th>161</th>
      <td>7.25</td>
    </tr>
    <tr>
      <th>162</th>
      <td>6.12</td>
    </tr>
    <tr>
      <th>163</th>
      <td>9.06</td>
    </tr>
    <tr>
      <th>164</th>
      <td>1.92</td>
    </tr>
    <tr>
      <th>165</th>
      <td>10.11</td>
    </tr>
    <tr>
      <th>166</th>
      <td>12.75</td>
    </tr>
    <tr>
      <th>167</th>
      <td>4.76</td>
    </tr>
    <tr>
      <th>168</th>
      <td>2.64</td>
    </tr>
    <tr>
      <th>169</th>
      <td>13.28</td>
    </tr>
    <tr>
      <th>170</th>
      <td>9.90</td>
    </tr>
    <tr>
      <th>171</th>
      <td>18.10</td>
    </tr>
    <tr>
      <th>172</th>
      <td>11.83</td>
    </tr>
    <tr>
      <th>173</th>
      <td>24.15</td>
    </tr>
    <tr>
      <th>174</th>
      <td>12.30</td>
    </tr>
    <tr>
      <th>175</th>
      <td>11.16</td>
    </tr>
    <tr>
      <th>176</th>
      <td>11.88</td>
    </tr>
    <tr>
      <th>177</th>
      <td>19.56</td>
    </tr>
    <tr>
      <th>178</th>
      <td>4.82</td>
    </tr>
    <tr>
      <th>179</th>
      <td>13.16</td>
    </tr>
    <tr>
      <th>180</th>
      <td>13.90</td>
    </tr>
    <tr>
      <th>181</th>
      <td>13.68</td>
    </tr>
    <tr>
      <th>182</th>
      <td>17.40</td>
    </tr>
    <tr>
      <th>183</th>
      <td>11.80</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 1 columns</p>
</div>




```python
#Merging purchase count & purchase value
itemmerge = pd.merge(itemID, itemtotal, left_index = True, right_index = True)
itemmerge
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>9</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
      <td>13.41</td>
    </tr>
    <tr>
      <th>34</th>
      <td>9</td>
      <td>37.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Dropping duplicates
dupitem = pdata.drop_duplicates(['Item ID'], keep = 'last')
dupitem
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>age_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>59</th>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>63</th>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>88</th>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>129</th>
      <td>23</td>
      <td>Female</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>3.25</td>
      <td>Eurinu48</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>173</th>
      <td>30</td>
      <td>Male</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>185</th>
      <td>22</td>
      <td>Male</td>
      <td>167</td>
      <td>Malice, Legacy of the Queen</td>
      <td>2.38</td>
      <td>Siarinum43</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>196</th>
      <td>20</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>1.50</td>
      <td>Chanirra56</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>205</th>
      <td>17</td>
      <td>Male</td>
      <td>147</td>
      <td>Hellreaver, Heirloom of Inception</td>
      <td>3.59</td>
      <td>Airidil41</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>239</th>
      <td>24</td>
      <td>Female</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>3.03</td>
      <td>Ethruard50</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>253</th>
      <td>15</td>
      <td>Male</td>
      <td>149</td>
      <td>Tranquility, Razor of Black Magic</td>
      <td>2.47</td>
      <td>Meosridil82</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>256</th>
      <td>22</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>3.47</td>
      <td>Iadueria43</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>300</th>
      <td>15</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Lisossan98</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>315</th>
      <td>24</td>
      <td>Male</td>
      <td>54</td>
      <td>Eternal Cleaver</td>
      <td>3.14</td>
      <td>Aelin32</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>336</th>
      <td>15</td>
      <td>Male</td>
      <td>173</td>
      <td>Stormfury Longsword</td>
      <td>4.83</td>
      <td>Iskadarya95</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>341</th>
      <td>20</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>2.04</td>
      <td>Aeliriarin93</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>342</th>
      <td>15</td>
      <td>Female</td>
      <td>50</td>
      <td>Dawn</td>
      <td>2.55</td>
      <td>Raedalis34</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>387</th>
      <td>24</td>
      <td>Female</td>
      <td>51</td>
      <td>Endbringer</td>
      <td>2.67</td>
      <td>Ethruard50</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>398</th>
      <td>25</td>
      <td>Female</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>4.77</td>
      <td>Tyaelistidru84</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>401</th>
      <td>17</td>
      <td>Male</td>
      <td>121</td>
      <td>Massacre</td>
      <td>3.42</td>
      <td>Leulaesti78</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>411</th>
      <td>25</td>
      <td>Male</td>
      <td>7</td>
      <td>Thorn, Satchel of Dark Souls</td>
      <td>4.51</td>
      <td>Saedue76</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>419</th>
      <td>25</td>
      <td>Female</td>
      <td>42</td>
      <td>The Decapitator</td>
      <td>4.82</td>
      <td>Tyeuladeu30</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>421</th>
      <td>22</td>
      <td>Male</td>
      <td>150</td>
      <td>Deathraze</td>
      <td>4.54</td>
      <td>Ina92</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>422</th>
      <td>24</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.92</td>
      <td>Saida58</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>423</th>
      <td>32</td>
      <td>Other / Non-Disclosed</td>
      <td>29</td>
      <td>Chaos, Ender of the End</td>
      <td>3.79</td>
      <td>Aithelis62</td>
      <td>30 - 34</td>
    </tr>
    <tr>
      <th>430</th>
      <td>27</td>
      <td>Male</td>
      <td>74</td>
      <td>Yearning Crusher</td>
      <td>1.06</td>
      <td>Lirtassa47</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>436</th>
      <td>10</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>4.82</td>
      <td>Ethrusuard41</td>
      <td>10 - 14</td>
    </tr>
    <tr>
      <th>446</th>
      <td>22</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>Lisosianya62</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>746</th>
      <td>35</td>
      <td>Male</td>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>Ralasti48</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>748</th>
      <td>15</td>
      <td>Male</td>
      <td>120</td>
      <td>Agatha</td>
      <td>1.91</td>
      <td>Isri49</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>749</th>
      <td>21</td>
      <td>Male</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>1.79</td>
      <td>Frichassala85</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>750</th>
      <td>23</td>
      <td>Male</td>
      <td>86</td>
      <td>Stormfury Lantern</td>
      <td>1.28</td>
      <td>Eollym91</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>752</th>
      <td>15</td>
      <td>Female</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>2.37</td>
      <td>Yalostiphos68</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>753</th>
      <td>20</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>Thryallym62</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>755</th>
      <td>22</td>
      <td>Female</td>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>1.88</td>
      <td>Ailaesuir66</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>756</th>
      <td>22</td>
      <td>Male</td>
      <td>6</td>
      <td>Rusty Skull</td>
      <td>1.20</td>
      <td>Siasri67</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>757</th>
      <td>35</td>
      <td>Male</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Seosri62</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>759</th>
      <td>19</td>
      <td>Male</td>
      <td>87</td>
      <td>Deluge, Edge of the West</td>
      <td>2.20</td>
      <td>Chanirrasta87</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>760</th>
      <td>29</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>Aerithllora36</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>761</th>
      <td>28</td>
      <td>Male</td>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>Raeduerin33</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>762</th>
      <td>36</td>
      <td>Male</td>
      <td>52</td>
      <td>Hatred</td>
      <td>4.39</td>
      <td>Lisosiast26</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>763</th>
      <td>27</td>
      <td>Other / Non-Disclosed</td>
      <td>48</td>
      <td>Rage, Legacy of the Lone Victor</td>
      <td>4.32</td>
      <td>Eurisuru25</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>764</th>
      <td>25</td>
      <td>Male</td>
      <td>70</td>
      <td>Hope's End</td>
      <td>3.89</td>
      <td>Assassasda84</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>765</th>
      <td>15</td>
      <td>Male</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aerithnucal56</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>766</th>
      <td>22</td>
      <td>Female</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>Nitherian58</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>767</th>
      <td>20</td>
      <td>Male</td>
      <td>122</td>
      <td>Unending Tyranny</td>
      <td>1.21</td>
      <td>Hailaphos89</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>768</th>
      <td>21</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>3.56</td>
      <td>Chamucosda93</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>769</th>
      <td>24</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>3.74</td>
      <td>Frichilsasya78</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>770</th>
      <td>22</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.27</td>
      <td>Aenasu69</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>771</th>
      <td>24</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>1.03</td>
      <td>Lassista97</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>772</th>
      <td>15</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Sidap51</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>773</th>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>Chamadarsda63</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>774</th>
      <td>24</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Lassassast73</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>775</th>
      <td>22</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>3.62</td>
      <td>Eural50</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>776</th>
      <td>14</td>
      <td>Male</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1.36</td>
      <td>Lirtossa78</td>
      <td>10 - 14</td>
    </tr>
    <tr>
      <th>777</th>
      <td>20</td>
      <td>Male</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.15</td>
      <td>Tillyrin30</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>778</th>
      <td>20</td>
      <td>Male</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>1.72</td>
      <td>Quelaton80</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>779</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>Alim85</td>
      <td>20 - 24</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 7 columns</p>
</div>




```python
#Merging to get all information from top 6
mergeID = pd.merge(itemmerge, dupitems, left_index = True, right_on = 'Item ID')
mergeID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item ID_x</th>
      <th>Price_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID_y</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>age_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>721</th>
      <td>39</td>
      <td>11</td>
      <td>25.85</td>
      <td>26</td>
      <td>Male</td>
      <td>39</td>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>2.35</td>
      <td>Aeduera68</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>766</th>
      <td>84</td>
      <td>11</td>
      <td>24.53</td>
      <td>22</td>
      <td>Female</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>Nitherian58</td>
      <td>20 - 24</td>
    </tr>
    <tr>
      <th>772</th>
      <td>31</td>
      <td>9</td>
      <td>18.63</td>
      <td>15</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>2.07</td>
      <td>Sidap51</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>761</th>
      <td>175</td>
      <td>9</td>
      <td>11.16</td>
      <td>28</td>
      <td>Male</td>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>1.24</td>
      <td>Raeduerin33</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>765</th>
      <td>13</td>
      <td>9</td>
      <td>13.41</td>
      <td>15</td>
      <td>Male</td>
      <td>13</td>
      <td>Serenity</td>
      <td>1.49</td>
      <td>Aerithnucal56</td>
      <td>15 - 19</td>
    </tr>
    <tr>
      <th>746</th>
      <td>34</td>
      <td>9</td>
      <td>37.26</td>
      <td>35</td>
      <td>Male</td>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>Ralasti48</td>
      <td>35 - 39</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Columns needed
mergeID = mergeID[['Item ID', 'Item Name', 'Item ID_x', 'Price_y', 'Price_x']]
mergeID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Item ID_x</th>
      <th>Price_y</th>
      <th>Price_x</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>721</th>
      <td>39</td>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>2.35</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>766</th>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>2.23</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>772</th>
      <td>31</td>
      <td>Trickster</td>
      <td>9</td>
      <td>2.07</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>761</th>
      <td>175</td>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>1.24</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>765</th>
      <td>13</td>
      <td>Serenity</td>
      <td>9</td>
      <td>1.49</td>
      <td>13.41</td>
    </tr>
    <tr>
      <th>746</th>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Resetting index as item ID for aesthetics
mergeID.set_index(["Item ID"], inplace = True)
mergeID
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item ID_x</th>
      <th>Price_y</th>
      <th>Price_x</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>2.35</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>2.23</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Trickster</td>
      <td>9</td>
      <td>2.07</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>1.24</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Serenity</td>
      <td>9</td>
      <td>1.49</td>
      <td>13.41</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Renaming Columns
mergeID.rename(columns =  {'Item ID_x': 'Purchase Count', 'Price_y': 'Item Price', 'Price_x': 'Total Purchase Value'}, inplace=True)
mergeID
```

    /Users/sundayjoseph/anaconda3/lib/python3.6/site-packages/pandas/core/frame.py:2746: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      **kwargs)





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>2.35</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>2.23</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Trickster</td>
      <td>9</td>
      <td>2.07</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>1.24</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Serenity</td>
      <td>9</td>
      <td>1.49</td>
      <td>13.41</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
  </tbody>
</table>
</div>



MOST PROFITABLE ITEMS
#Identify the 5 most profitable items by total purchase value, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value


```python
#Total purchase value by high - low
pvalue = pd.DataFrame(pdata.groupby('Item ID')['Price'].sum())
pvalue.sort_values("Price", ascending = False, inplace = True)
pvalue
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>28.88</td>
    </tr>
    <tr>
      <th>101</th>
      <td>27.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>27.06</td>
    </tr>
    <tr>
      <th>145</th>
      <td>26.70</td>
    </tr>
    <tr>
      <th>39</th>
      <td>25.85</td>
    </tr>
    <tr>
      <th>152</th>
      <td>25.20</td>
    </tr>
    <tr>
      <th>102</th>
      <td>24.96</td>
    </tr>
    <tr>
      <th>158</th>
      <td>24.92</td>
    </tr>
    <tr>
      <th>66</th>
      <td>24.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>24.53</td>
    </tr>
    <tr>
      <th>173</th>
      <td>24.15</td>
    </tr>
    <tr>
      <th>128</th>
      <td>24.00</td>
    </tr>
    <tr>
      <th>148</th>
      <td>23.76</td>
    </tr>
    <tr>
      <th>46</th>
      <td>23.75</td>
    </tr>
    <tr>
      <th>108</th>
      <td>23.73</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23.46</td>
    </tr>
    <tr>
      <th>153</th>
      <td>22.85</td>
    </tr>
    <tr>
      <th>73</th>
      <td>22.44</td>
    </tr>
    <tr>
      <th>91</th>
      <td>22.26</td>
    </tr>
    <tr>
      <th>48</th>
      <td>21.60</td>
    </tr>
    <tr>
      <th>12</th>
      <td>21.50</td>
    </tr>
    <tr>
      <th>22</th>
      <td>21.42</td>
    </tr>
    <tr>
      <th>49</th>
      <td>21.15</td>
    </tr>
    <tr>
      <th>30</th>
      <td>20.75</td>
    </tr>
    <tr>
      <th>121</th>
      <td>20.52</td>
    </tr>
    <tr>
      <th>81</th>
      <td>20.30</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>149</th>
      <td>4.94</td>
    </tr>
    <tr>
      <th>24</th>
      <td>4.82</td>
    </tr>
    <tr>
      <th>178</th>
      <td>4.82</td>
    </tr>
    <tr>
      <th>167</th>
      <td>4.76</td>
    </tr>
    <tr>
      <th>116</th>
      <td>4.74</td>
    </tr>
    <tr>
      <th>82</th>
      <td>4.44</td>
    </tr>
    <tr>
      <th>25</th>
      <td>4.12</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.08</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.96</td>
    </tr>
    <tr>
      <th>122</th>
      <td>3.63</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.60</td>
    </tr>
    <tr>
      <th>147</th>
      <td>3.59</td>
    </tr>
    <tr>
      <th>41</th>
      <td>3.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>136</th>
      <td>3.30</td>
    </tr>
    <tr>
      <th>126</th>
      <td>3.25</td>
    </tr>
    <tr>
      <th>109</th>
      <td>3.20</td>
    </tr>
    <tr>
      <th>69</th>
      <td>3.18</td>
    </tr>
    <tr>
      <th>28</th>
      <td>3.04</td>
    </tr>
    <tr>
      <th>89</th>
      <td>3.00</td>
    </tr>
    <tr>
      <th>72</th>
      <td>2.78</td>
    </tr>
    <tr>
      <th>168</th>
      <td>2.64</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2.38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
    <tr>
      <th>74</th>
      <td>2.12</td>
    </tr>
    <tr>
      <th>164</th>
      <td>1.92</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>59</th>
      <td>1.65</td>
    </tr>
    <tr>
      <th>156</th>
      <td>1.16</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 1 columns</p>
</div>




```python
pvalue = pvalue.iloc[0:5][:]
pvalue
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Item purchase count
itempcount= pd.DataFrame(pdata.groupby('Item ID')['Item ID'].count())
itempcount
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4</td>
    </tr>
    <tr>
      <th>17</th>
      <td>3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <td>4</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
    </tr>
    <tr>
      <th>22</th>
      <td>6</td>
    </tr>
    <tr>
      <th>23</th>
      <td>4</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>4</td>
    </tr>
    <tr>
      <th>26</th>
      <td>4</td>
    </tr>
    <tr>
      <th>27</th>
      <td>4</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>154</th>
      <td>7</td>
    </tr>
    <tr>
      <th>155</th>
      <td>3</td>
    </tr>
    <tr>
      <th>156</th>
      <td>1</td>
    </tr>
    <tr>
      <th>157</th>
      <td>4</td>
    </tr>
    <tr>
      <th>158</th>
      <td>7</td>
    </tr>
    <tr>
      <th>159</th>
      <td>5</td>
    </tr>
    <tr>
      <th>160</th>
      <td>5</td>
    </tr>
    <tr>
      <th>161</th>
      <td>5</td>
    </tr>
    <tr>
      <th>162</th>
      <td>3</td>
    </tr>
    <tr>
      <th>163</th>
      <td>3</td>
    </tr>
    <tr>
      <th>164</th>
      <td>1</td>
    </tr>
    <tr>
      <th>165</th>
      <td>3</td>
    </tr>
    <tr>
      <th>166</th>
      <td>3</td>
    </tr>
    <tr>
      <th>167</th>
      <td>2</td>
    </tr>
    <tr>
      <th>168</th>
      <td>1</td>
    </tr>
    <tr>
      <th>169</th>
      <td>4</td>
    </tr>
    <tr>
      <th>170</th>
      <td>5</td>
    </tr>
    <tr>
      <th>171</th>
      <td>5</td>
    </tr>
    <tr>
      <th>172</th>
      <td>7</td>
    </tr>
    <tr>
      <th>173</th>
      <td>5</td>
    </tr>
    <tr>
      <th>174</th>
      <td>5</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
    </tr>
    <tr>
      <th>176</th>
      <td>4</td>
    </tr>
    <tr>
      <th>177</th>
      <td>4</td>
    </tr>
    <tr>
      <th>178</th>
      <td>2</td>
    </tr>
    <tr>
      <th>179</th>
      <td>7</td>
    </tr>
    <tr>
      <th>180</th>
      <td>5</td>
    </tr>
    <tr>
      <th>181</th>
      <td>3</td>
    </tr>
    <tr>
      <th>182</th>
      <td>5</td>
    </tr>
    <tr>
      <th>183</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 1 columns</p>
</div>




```python
#Merging 
pvalue = pd.merge(pvalue, itempcount, left_index = True, right_index = True, how = 'left')
pvalue
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>37.26</td>
      <td>9</td>
    </tr>
    <tr>
      <th>115</th>
      <td>29.75</td>
      <td>7</td>
    </tr>
    <tr>
      <th>32</th>
      <td>29.70</td>
      <td>6</td>
    </tr>
    <tr>
      <th>103</th>
      <td>29.22</td>
      <td>6</td>
    </tr>
    <tr>
      <th>107</th>
      <td>28.88</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merging top 5 rows
mergeprofit = pd.merge(pvalue, dupitem, left_index = True, right_on = 'Item ID', how = 'left')
mergeprofit
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Price_x</th>
      <th>Item ID_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID_y</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>age_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>746</th>
      <td>34</td>
      <td>37.26</td>
      <td>9</td>
      <td>35</td>
      <td>Male</td>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>Ralasti48</td>
      <td>35 - 39</td>
    </tr>
    <tr>
      <th>705</th>
      <td>115</td>
      <td>29.75</td>
      <td>7</td>
      <td>25</td>
      <td>Male</td>
      <td>115</td>
      <td>Spectral Diamond Doomblade</td>
      <td>4.25</td>
      <td>Aeral85</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>657</th>
      <td>32</td>
      <td>29.70</td>
      <td>6</td>
      <td>28</td>
      <td>Male</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>4.95</td>
      <td>Tyarithn67</td>
      <td>25 - 29</td>
    </tr>
    <tr>
      <th>716</th>
      <td>103</td>
      <td>29.22</td>
      <td>6</td>
      <td>9</td>
      <td>Male</td>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>4.87</td>
      <td>Ilophos58</td>
      <td>&lt; 10</td>
    </tr>
    <tr>
      <th>779</th>
      <td>107</td>
      <td>28.88</td>
      <td>8</td>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>3.61</td>
      <td>Alim85</td>
      <td>20 - 24</td>
    </tr>
  </tbody>
</table>
</div>




```python
mergeprofit = mergeprofit[['Item ID', 'Item Name', 'Item ID_x', 'Price_y','Price_x']]
mergeprofit
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Item ID_x</th>
      <th>Price_y</th>
      <th>Price_x</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>746</th>
      <td>34</td>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>705</th>
      <td>115</td>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>657</th>
      <td>32</td>
      <td>Orenmir</td>
      <td>6</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>716</th>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>6</td>
      <td>4.87</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>779</th>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>8</td>
      <td>3.61</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
mergeprofit.set_index(['Item ID'], inplace=True)
mergeprofit
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item ID_x</th>
      <th>Price_y</th>
      <th>Price_x</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Singed Scalpel</td>
      <td>6</td>
      <td>4.87</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Splitter, Foe Of Subtlety</td>
      <td>8</td>
      <td>3.61</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
mergeprofit.rename(columns = {'Item ID_x': 'Purchase Count', 'Price_y': 'Item Price', 'Price_x': 'Total Purchase Value'}, inplace = True)
mergeprofit
```

    /Users/sundayjoseph/anaconda3/lib/python3.6/site-packages/pandas/core/frame.py:2746: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      **kwargs)





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Singed Scalpel</td>
      <td>6</td>
      <td>4.87</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Splitter, Foe Of Subtlety</td>
      <td>8</td>
      <td>3.61</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
OBSERVATIONS

On the Gender Demographics, males make up over 80 percent of players. The males also make over 80% of the revenue.

Player spend under $20 on item out 573.

Between 25 to 29 age group purchase more expensive items on average.

```
