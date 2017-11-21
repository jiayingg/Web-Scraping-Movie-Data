

```python
from bs4 import BeautifulSoup
import pandas as pd
```


```python
## Lionsgate [us] (Distributor)

url = "http://www.imdb.com/company/co0173285/?ref_=fn_al_co_1"
response = requests.get(url)
html_soup = BeautifulSoup(response.text, 'html.parser')
```


```python
lionsgate = html_soup.find_all("ol")
Distributor = lionsgate[0].find_all("a")
Production = lionsgate[1].find_all("a")
Miscellaneous = lionsgate[2].find_all("a")
print(len(Distributor), len(Production), len(Miscellaneous))
```

    841 268 41
    


```python
href = []
names = []
years = []
imdb_ratings = []
votes = []

for i in range(1, len(Production)):
    href.append("http://www.imdb.com/" + Production[i]["href"])
    names.append(Production[i].text)
    print(i, Production[i].text)
    url2 = "http://www.imdb.com/" + Production[i]["href"]
    response2 = requests.get(url2)
    html_soup2 = BeautifulSoup(response2.text, 'html.parser')
    
###### Year #################################################################################
    year = html_soup2.find_all('div', class_ = 'title_wrapper')
    if(year == [] or year[0].h1.a is None):
        years.append(None)
    else:
        years.append(int(year[0].h1.a.text))
    
###### Rating ##############################################################################
    rating = html_soup2.find_all('div', class_ = 'imdbRating')
    if(rating == [] or rating[0].strong is None):
        imdb_ratings.append(None)
    else:
        imdb_ratings.append(float(rating[0].strong.span.text))
    
###### Votes ###############################################################################
    vote = html_soup2.find_all('div', class_ = 'imdbRating')
    if(vote == [] or vote[0].a is None):
        votes.append(None)
    else:
        votes.append(int(vote[0].a.span.text.replace(",", "")))
```

    1 Now You See Me 3
    2 Robin Hood
    3 The Spy Who Dumped Me
    4 12 Strong
    5 Escape Plan 2: Hades
    6 Honored
    7 "Kevin Hart: What The Fit"
    8 Kin
    9 Most Likely to Murder
    10 Love Beats Rhymes
    11 "MacGyver: Packing Peanuts + Fire (#2.8)"
    12 Wonder
    13 "MacGyver: Duct Tape + Jack (#2.7)"
    14 "MacGyver: Jet Engine + Pickup Truck (#2.6)"
    15 "MacGyver: Skull + Electromagnet (#2.5)"
    16 "MacGyver: X-Ray + Penny (#2.4)"
    17 "MacGyver: Roulette Wheel + Wire (#2.3)"
    18 "MacGyver: Muscle Car + Paper Clips (#2.2)"
    19 My Little Pony: The Movie
    20 "MacGyver: DIY or DIE (#2.1)"
    21 "Manhunt: Unabomber: USA vs. Theodore J. Kaczynski (#1.8)"
    22 Stronger
    23 American Assassin
    24 "Manhunt: Unabomber: Lincoln (#1.7)"
    25 "Manhunt: Unabomber: Ted (#1.6)"
    26 Leatherface
    27 "Manhunt: Unabomber: Abri (#1.5)"
    28 "Manhunt: Unabomber: Publish or Perish (#1.4)"
    29 The Glass Castle
    30 "Manhunt: Unabomber: Fruit of the Poisonous Tree (#1.3)"
    31 "Manhunt: Unabomber: Pure Wudder (#1.2)"
    32 "Manhunt: Unabomber: UNABOM (#1.1)"
    33 Alpha and Omega: Journey to Bear Kingdom
    34 "MacGyver: Cigar Cutter (#1.21)"
    35 "MacGyver: Hole Puncher (#1.20)"
    36 "MacGyver: Compass (#1.19)"
    37 Power Rangers: Legacy Wars
    38 Power Rangers
    39 "MacGyver: Flashlight (#1.18)"
    40 Out of the Bottle
    41 The Djinn and Alexandra
    42 The Magic Words
    43 "MacGyver: Ruler (#1.17)"
    44 "MacGyver: Hook (#1.16)"
    45 "MacGyver: Magnifying Glass (#1.15)"
    46 "MacGyver: Fish Scaler (#1.14)"
    47 Cutting for Ken
    48 Inside Out: An Interview with Director of Photography Robin Vidgeon
    49 Leftovers to Be with Screenwriter Christopher Hawthorne
    50 Mary, Mary: An Interview with Actress Sammi Davis
    51 Mother's Day with Actress Mary Beth Hurt
    52 Tyler Perry's: Madea on the Run
    53 Vintage Tastes with Decorative Consultant Yolanda Cuomo
    54 Worm Food: The Effects of the Lair of the White Worm
    55 John Wick: Chapter 2
    56 "MacGyver: Large Blade (#1.13)"
    57 "MacGyver: Screwdriver (#1.12)"
    58 "American Lion"
    59 "Kicking & Screaming"
    60 Public Disturbance
    61 "Step Up: High Water"
    62 "MacGyver: Scissors (#1.11)"
    63 "MacGyver: Pliers (#1.10)"
    64 "MacGyver: Chisel (#1.9)"
    65 "MacGyver: Corkscrew (#1.8)"
    66 Alpha and Omega 7: The Big Fureeze
    67 "MacGyver: Can Opener (#1.7)"
    68 "MacGyver: Wrench (#1.6)"
    69 "MacGyver: Toothpick (#1.5)"
    70 "MacGyver: Wire Cutter (#1.4)"
    71 "MacGyver: Awl (#1.3)"
    72 "MacGyver: Metal Saw (#1.2)"
    73 "MacGyver"
    74 "MacGyver: The Rising (#1.1)"
    75 Blair Witch
    76 "Tracks"
    77 "Join or Die with Craig Ferguson: History's Biggest Douchebag (#1.22)"
    78 Nerve
    79 "Join or Die with Craig Ferguson: History's Biggest Badass (#1.21)"
    80 "Join or Die with Craig Ferguson: History's Biggest Fraud (#1.20)"
    81 "Join or Die with Craig Ferguson: History's Best Founding Fathers (#1.19)"
    82 "Join or Die with Craig Ferguson: History's Most Defiant Moments of the Last 75 Years (#1.18)"
    83 "Join or Die with Craig Ferguson: History's Greatest Gangster (#1.17)"
    84 "Join or Die with Craig Ferguson: History's Greatest Unexplained Phenomenon (#1.16)"
    85 "Join or Die with Craig Ferguson: History's Dumbest Mistake (#1.14)"
    86 "Join or Die with Craig Ferguson: History's Greatest Unsolved Mystery (#1.15)"
    87 "Join or Die with Craig Ferguson: History's Biggest Presidential Bad Boy (#1.13)"
    88 "Join or Die with Craig Ferguson: History's Most Plausible Conspiracy Theory (#1.12)"
    89 "Join or Die with Craig Ferguson: History's Greatest Man-Made Structure (#1.11)"
    90 "Greenleaf"
    91 "Join or Die with Craig Ferguson: History's Biggest Fall from Grace (#1.10)"
    92 "Join or Die with Craig Ferguson: The Drug That Changed the World (#1.9)"
    93 Criminal
    94 "Join or Die with Craig Ferguson: History's Most Influential Band (#1.8)"
    95 "Join or Die with Craig Ferguson: History's Greatest Invention Since 1950 (#1.7)"
    96 "Join or Die with Craig Ferguson: History's Craziest Cult (#1.6)"
    97 "Join or Die with Craig Ferguson: History's Worst Tyrant (#1.5)"
    98 "Join or Die with Craig Ferguson: History's Most Doomed Presidential Campaign (#1.4)"
    99 "Join or Die with Craig Ferguson: History's Biggest Frenemies (#1.3)"
    100 "Join or Die with Craig Ferguson"
    101 "Join or Die with Craig Ferguson: History's Biggest Political Blunder (#1.1)"
    102 "Join or Die with Craig Ferguson: History's Worst Medical Advice (#1.2)"
    103 Dirty Grandpa
    104 Norm of the North
    105 Aztec Warrior
    106 The Making of Extraction
    107 The Art of Destruction: The Making of 'Knock Knock'
    108 "RocketJump: The Show"
    109 The Hunger Games: Mockingjay - Part 2
    110 Chain of Command
    111 The Vatican Tapes
    112 The Mary Alice Brandon File
    113 Twilight Storytellers: We've Met Before
    114 Sicario
    115 Maggie
    116 The Lazarus Effect
    117 A Day in the Life of Little House
    118 Wild Card
    119 The Hunger Games: Mockingjay - Part 1
    120 Jessabelle
    121 SPYMASTER: John le Carré in Hamburg
    122 See No Evil 2
    123 Addicted
    124 Alpha and Omega 4: The Legend of the Saw Toothed Cave
    125 Beyond the Reach
    126 The Expendables 3
    127 My Man Is a Loser
    128 "Deal with It: Tom Green and WWE's the Miz (#2.12)"
    129 "Deal with It: Bill & Giuliana Rancic and Alex Mandel (#2.11)"
    130 "Deal with It: David Koechner and Alex Mandel (#2.10)"
    131 "Deal with It: Kelly Osbourne and Moshe Kasher (#2.9)"
    132 "Deal with It: Howie Mandel and Kevin Nealon (#2.8)"
    133 "Deal with It: Bob Saget and Chuey Martinez (#2.7)"
    134 "Deal with It: Arsenio Hall and Alex Mandel (#2.6)"
    135 "Deal with It: Chris Jericho and Bill Engvall (#2.5)"
    136 Draft Day
    137 The Single Moms Club
    138 They Came Together
    139 The Little House Phenomenon: A Place in Television History
    140 I, Frankenstein
    141 A Most Wanted Man
    142 The Hunger Games: Catching Fire
    143 Nurse 3D
    144 "Deal with It"
    145 Burning Blue
    146 Rapture-Palooza
    147 "Family Trade: Episode #1.8"
    148 "Family Trade: Episode #1.7"
    149 Redemption
    150 "Family Trade: Episode #1.6"
    151 "Family Trade: Episode #1.5"
    152 "Family Trade: Episode #1.4"
    153 "Family Trade: Episode #1.3"
    154 Temptation: Confessions of a Marriage Counselor
    155 "Family Trade"
    156 "Family Trade: Episode #1.1"
    157 "Family Trade: Episode #1.2"
    158 Texas Chainsaw 3D
    159 Stand Up Guys
    160 How to Survive a Horror Film: Cabin in the Woods
    161 Mud
    162 What to Expect When You're Expecting
    163 Safe
    164 Casa de mi Padre
    165 The Hunger Games
    166 The Cabin in the Woods
    167 Good Deeds
    168 Arbitrage
    169 A Madea Christmas
    170 Fred 2: Night of the Living Fred
    171 Warrior
    172 Abduction
    173 Thor: Tales of Asgard
    174 The Lincoln Lawyer
    175 From Prada to Nada
    176 Leapfrog: The Amazing Alphabet Amusement Park
    177 Jane Fonda: Prime Time - Fit & Strong
    178 Jane Fonda: Prime Time - Walkout
    179 The Next Three Days
    180 For Colored Girls
    181 Beatdown
    182 Burning Bright
    183 Killers
    184 Adventures in Acting with the Kids of 'The Spy Next Door'
    185 Jackie Chan: Stunt Master and Mentor
    186 Medgar Evers: An Unsung Hero
    187 Why Did I Get Married Too?
    188 Unrivaled
    189 Planet Hulk
    190 No Greater Love
    191 Brothers
    192 Daybreakers
    193 Gamer
    194 LeapFrog: Let's Go to School
    195 Crank: High Voltage
    196 The Spirit: History Repeats
    197 The Haunting in Connecticut
    198 New in Town
    199 Precious
    200 Tenderness
    201 "Crash: The Pain Won't Stop (#1.13)"
    202 My Bloody Valentine
    203 "Crash: Ring Dings (#1.12)"
    204 "Crash: TF-36, Sprint Left, T-4 (#1.11)"
    205 The Spirit
    206 "Crash: The Future Is Free (#1.10)"
    207 "Crash: Pissing in the Sandbox (#1.9)"
    208 "Crash: Three Men and a Bebe (#1.8)"
    209 Punisher: War Zone
    210 "Crash: Los Muertos (#1.7)"
    211 "Crash: Clusterf**k (#1.6)"
    212 Thomas Kinkade's Christmas Cottage
    213 "Crash: Your Ass Belongs to the Gypsies (#1.5)"
    214 "50 Cent: The Money and the Power"
    215 "Crash: Railroaded (#1.4)"
    216 "Crash: Panic (#1.3)"
    217 "Crash: Episode One (#1.1)"
    218 "Crash: The Doctor Is In (#1.2)"
    219 W.
    220 Divina confusión
    221 My Best Friend's Girl
    222 Disaster Movie
    223 The Midnight Meat Train
    224 Amor letra por letra
    225 Jillian Michaels - 30 Day Shred
    226 The Lucky Ones
    227 The Eye
    228 Rambo
    229 War
    230 3:10 to Yuma
    231 Doctor Strange
    232 Monster Squad Forever!
    233 Catacombs
    234 Good Luck Chuck
    235 Hostel: Part II
    236 The Condemned
    237 Pride
    238 The Invincible Iron Man
    239 Trade
    240 Happily N'Ever After
    241 Employee of the Month
    242 Controversial Confection: The Soul of 'Hard Candy'
    243 Creating 'Hard Candy'
    244 The U.S. vs. John Lennon
    245 Ultimate Avengers II
    246 Skinwalkers
    247 Right at Your Door
    248 Leonard Cohen: I'm Your Man
    249 Bob the Builder: Tool Power!
    250 "Magic Adventures of Mumfie"
    251 Action #1
    252 Ballerina
    253 Dirty Dancing
    254 Flyy
    255 Heist Society
    256 Luckiest Girl Alive
    257 Monopoly
    258 Naruto
    259 New People
    260 Starfall
    261 The Divergent Series: Ascendant
    262 The Game
    263 The Kingkiller Chronicle
    264 Two Eyes Staring
    265 Untitled Time Travel Project
    266 White Girl Problems
    267 XOXO
    


```python
production = pd.DataFrame({'names': names,
                           'href': href,
                           'year': years,
                           'rating': imdb_ratings,
                           'votes': votes})
```


```python
production
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
      <th>href</th>
      <th>names</th>
      <th>rating</th>
      <th>votes</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>http://www.imdb.com//title/tt4712810/</td>
      <td>Now You See Me 3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2019.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>http://www.imdb.com//title/tt4532826/</td>
      <td>Robin Hood</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>http://www.imdb.com//title/tt6663582/</td>
      <td>The Spy Who Dumped Me</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>http://www.imdb.com//title/tt1413492/</td>
      <td>12 Strong</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>http://www.imdb.com//title/tt6513656/</td>
      <td>Escape Plan 2: Hades</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>http://www.imdb.com//title/tt7237666/</td>
      <td>Honored</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>http://www.imdb.com//title/tt7395586/</td>
      <td>"Kevin Hart: What The Fit"</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>http://www.imdb.com//title/tt6017942/</td>
      <td>Kin</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>http://www.imdb.com//title/tt6566830/</td>
      <td>Most Likely to Murder</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>http://www.imdb.com//title/tt4686108/</td>
      <td>Love Beats Rhymes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>http://www.imdb.com//title/tt7477962/</td>
      <td>"MacGyver: Packing Peanuts + Fire (#2.8)"</td>
      <td>8.7</td>
      <td>36.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>http://www.imdb.com//title/tt2543472/</td>
      <td>Wonder</td>
      <td>7.9</td>
      <td>1146.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>http://www.imdb.com//title/tt7426112/</td>
      <td>"MacGyver: Duct Tape + Jack (#2.7)"</td>
      <td>8.0</td>
      <td>55.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>http://www.imdb.com//title/tt7318528/</td>
      <td>"MacGyver: Jet Engine + Pickup Truck (#2.6)"</td>
      <td>7.3</td>
      <td>72.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>http://www.imdb.com//title/tt7297054/</td>
      <td>"MacGyver: Skull + Electromagnet (#2.5)"</td>
      <td>7.7</td>
      <td>78.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>http://www.imdb.com//title/tt7234624/</td>
      <td>"MacGyver: X-Ray + Penny (#2.4)"</td>
      <td>7.8</td>
      <td>85.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>http://www.imdb.com//title/tt7151724/</td>
      <td>"MacGyver: Roulette Wheel + Wire (#2.3)"</td>
      <td>8.0</td>
      <td>96.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>http://www.imdb.com//title/tt7214180/</td>
      <td>"MacGyver: Muscle Car + Paper Clips (#2.2)"</td>
      <td>7.5</td>
      <td>78.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>http://www.imdb.com//title/tt4131800/</td>
      <td>My Little Pony: The Movie</td>
      <td>6.3</td>
      <td>3026.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>http://www.imdb.com//title/tt6687140/</td>
      <td>"MacGyver: DIY or DIE (#2.1)"</td>
      <td>7.0</td>
      <td>144.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>http://www.imdb.com//title/tt6528828/</td>
      <td>"Manhunt: Unabomber: USA vs. Theodore J. Kaczy...</td>
      <td>8.9</td>
      <td>124.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>http://www.imdb.com//title/tt3881784/</td>
      <td>Stronger</td>
      <td>7.5</td>
      <td>3015.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>http://www.imdb.com//title/tt1961175/</td>
      <td>American Assassin</td>
      <td>6.5</td>
      <td>13100.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>http://www.imdb.com//title/tt6528824/</td>
      <td>"Manhunt: Unabomber: Lincoln (#1.7)"</td>
      <td>8.6</td>
      <td>128.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>http://www.imdb.com//title/tt6528822/</td>
      <td>"Manhunt: Unabomber: Ted (#1.6)"</td>
      <td>8.9</td>
      <td>186.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>http://www.imdb.com//title/tt2620590/</td>
      <td>Leatherface</td>
      <td>5.1</td>
      <td>5766.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>http://www.imdb.com//title/tt6528820/</td>
      <td>"Manhunt: Unabomber: Abri (#1.5)"</td>
      <td>8.8</td>
      <td>150.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>http://www.imdb.com//title/tt6528816/</td>
      <td>"Manhunt: Unabomber: Publish or Perish (#1.4)"</td>
      <td>8.5</td>
      <td>150.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>http://www.imdb.com//title/tt2378507/</td>
      <td>The Glass Castle</td>
      <td>7.2</td>
      <td>7098.0</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>http://www.imdb.com//title/tt6491622/</td>
      <td>"Manhunt: Unabomber: Fruit of the Poisonous Tr...</td>
      <td>8.3</td>
      <td>161.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>237</th>
      <td>http://www.imdb.com//title/tt0903135/</td>
      <td>The Invincible Iron Man</td>
      <td>6.0</td>
      <td>6192.0</td>
      <td>2007.0</td>
    </tr>
    <tr>
      <th>238</th>
      <td>http://www.imdb.com//title/tt0399095/</td>
      <td>Trade</td>
      <td>7.4</td>
      <td>15536.0</td>
      <td>2007.0</td>
    </tr>
    <tr>
      <th>239</th>
      <td>http://www.imdb.com//title/tt0308353/</td>
      <td>Happily N'Ever After</td>
      <td>4.5</td>
      <td>9091.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>240</th>
      <td>http://www.imdb.com//title/tt0424993/</td>
      <td>Employee of the Month</td>
      <td>5.5</td>
      <td>39490.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>241</th>
      <td>http://www.imdb.com//title/tt1159927/</td>
      <td>Controversial Confection: The Soul of 'Hard Ca...</td>
      <td>6.6</td>
      <td>21.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>242</th>
      <td>http://www.imdb.com//title/tt1159209/</td>
      <td>Creating 'Hard Candy'</td>
      <td>7.6</td>
      <td>32.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>243</th>
      <td>http://www.imdb.com//title/tt0478049/</td>
      <td>The U.S. vs. John Lennon</td>
      <td>7.4</td>
      <td>4962.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>244</th>
      <td>http://www.imdb.com//title/tt0803093/</td>
      <td>Ultimate Avengers II</td>
      <td>6.7</td>
      <td>7713.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>245</th>
      <td>http://www.imdb.com//title/tt0461703/</td>
      <td>Skinwalkers</td>
      <td>4.6</td>
      <td>12079.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>246</th>
      <td>http://www.imdb.com//title/tt0458367/</td>
      <td>Right at Your Door</td>
      <td>6.2</td>
      <td>11505.0</td>
      <td>2006.0</td>
    </tr>
    <tr>
      <th>247</th>
      <td>http://www.imdb.com//title/tt0478197/</td>
      <td>Leonard Cohen: I'm Your Man</td>
      <td>6.9</td>
      <td>1921.0</td>
      <td>2005.0</td>
    </tr>
    <tr>
      <th>248</th>
      <td>http://www.imdb.com//title/tt1723006/</td>
      <td>Bob the Builder: Tool Power!</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2003.0</td>
    </tr>
    <tr>
      <th>249</th>
      <td>http://www.imdb.com//title/tt0361155/</td>
      <td>"Magic Adventures of Mumfie"</td>
      <td>7.9</td>
      <td>120.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>250</th>
      <td>http://www.imdb.com//title/tt2298239/</td>
      <td>Action #1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>251</th>
      <td>http://www.imdb.com//title/tt7181546/</td>
      <td>Ballerina</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>252</th>
      <td>http://www.imdb.com//title/tt1495731/</td>
      <td>Dirty Dancing</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>253</th>
      <td>http://www.imdb.com//title/tt2492524/</td>
      <td>Flyy</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>254</th>
      <td>http://www.imdb.com//title/tt1597724/</td>
      <td>Heist Society</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>255</th>
      <td>http://www.imdb.com//title/tt4595186/</td>
      <td>Luckiest Girl Alive</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>256</th>
      <td>http://www.imdb.com//title/tt1204976/</td>
      <td>Monopoly</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>257</th>
      <td>http://www.imdb.com//title/tt4907198/</td>
      <td>Naruto</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>258</th>
      <td>http://www.imdb.com//title/tt5580316/</td>
      <td>New People</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>259</th>
      <td>http://www.imdb.com//title/tt6173506/</td>
      <td>Starfall</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>260</th>
      <td>http://www.imdb.com//title/tt3663184/</td>
      <td>The Divergent Series: Ascendant</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>261</th>
      <td>http://www.imdb.com//title/tt0770826/</td>
      <td>The Game</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>262</th>
      <td>http://www.imdb.com//title/tt6292018/</td>
      <td>The Kingkiller Chronicle</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>263</th>
      <td>http://www.imdb.com//title/tt1732175/</td>
      <td>Two Eyes Staring</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>264</th>
      <td>http://www.imdb.com//title/tt3957732/</td>
      <td>Untitled Time Travel Project</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>265</th>
      <td>http://www.imdb.com//title/tt3014366/</td>
      <td>White Girl Problems</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>266</th>
      <td>http://www.imdb.com//title/tt1976655/</td>
      <td>XOXO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>267 rows × 5 columns</p>
</div>




```python
production.to_csv("production.csv", index = False)
```


```python

```
