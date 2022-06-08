Activity 8
================
Nick

## Data and packages

Load the entirety of the `{tidyverse}`. `{forcats}` and `{stringr}` are
loaded as part of this. If you wish to work with dates during this
activity, you will need to also load `{lubridate}`. Be sure to avoid
printing out any unnecessary information and give the code chunk a
meaningful name.

``` r
knitr::opts_chunk$set(error = TRUE)

library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.4     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.2     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

Cheatsheets that you might want to add to your collection:

-   [`{stringr}`](https://stringr.tidyverse.org/)
-   [`{forcats}`](https://forcats.tidyverse.org/)
-   [`{lubridate}`](https://lubridate.tidyverse.org/)

Using `here::here`, upload the `billboard_songs.txt` file that is saved
in your `data` folder. Notice that this file is a tab-delimited file
that is stored as a `.txt` file. Therefore, you will need to use either
`read_delim` with a `delim = ...` argument or (better) `read_tsv` .
Assign the file to a meaningful object name, be sure to avoid printing
any unnecessary information, and give the code chunk a meaningful name.

``` r
billboard_songs <- read_tsv(here::here("data","billboard_songs.txt"))
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   title = col_character(),
    ##   artist = col_character(),
    ##   `overall peak` = col_double(),
    ##   `weeks on chart` = col_double(),
    ##   `chart date` = col_double()
    ## )

These data include information on song popularity. In the US, the
Billboard Hot 100 is a list that comes out every week, showing the 100
most played songs that week. More information about the creation of this
dataset, as well as some analyses by the author, can be found here:
<https://mikekling.com/analyzing-the-billboard-hot-100/>. The dataset
you are provided is a limited version of the full data, containing:

-   `title`
-   `artist`
-   `overall peak`: The highest rank the song ever reached (1 is the
    best)
-   `weeks on chart`: The number of weeks the song was on the chart
-   `chart date`: The latest date the song appeared on the Billboard Hot
    100

This is a long dataset (34,605 observations)! You might like to create a
small dataset with only, say, 200 of the rows to try all your code out
on the smaller dataset first, and then only run the analysis of the full
data after you have experienced everything. One way to do this is to use
a function like `slice_sample(n = ...)` from `{dplyr}`.

``` r
smol_billboard <- billboard_songs %>%
slice_sample(n = 200)
```

If you wish to work with `{stringr}`, I find it useful to work on
vectors first. A way to do this is with `pull` from `{dplyr}`.

    # Turn variable from dataset into a vector
    dataset %>% 
      pull(variable)

``` r
smol_billboard %>%
  pull(title)
```

    ##   [1] "Delia Gone"                                              
    ##   [2] "Bang Bang"                                               
    ##   [3] "When The White Lilacs Bloom Again"                       
    ##   [4] "A Sign Of The Times"                                     
    ##   [5] "There I've Said It Again"                                
    ##   [6] "Let's Ride"                                              
    ##   [7] "We Played Games"                                         
    ##   [8] "Free Me From My Freedom / Tie Me To A Tree (Handcuff Me)"
    ##   [9] "Let's Go Get Stoned"                                     
    ##  [10] "Lonely Ol' Night"                                        
    ##  [11] "Keep On Dancing"                                         
    ##  [12] "Hard Times For Lovers"                                   
    ##  [13] "You Better Know It"                                      
    ##  [14] "Paradise"                                                
    ##  [15] "High School U.S.A."                                      
    ##  [16] "Gimme Some More"                                         
    ##  [17] "So Close"                                                
    ##  [18] "Surfin' U.S.A."                                          
    ##  [19] "Memories Of You"                                         
    ##  [20] "The Big Beat"                                            
    ##  [21] "Tequila"                                                 
    ##  [22] "I've Gotta Be Me"                                        
    ##  [23] "Love Like Crazy"                                         
    ##  [24] "That's When The Music Takes Me"                          
    ##  [25] "Theme From Mission Impossible"                           
    ##  [26] "If I Could See The Light"                                
    ##  [27] "Soft And Wet"                                            
    ##  [28] "Fall Away"                                               
    ##  [29] "Twine Time"                                              
    ##  [30] "Get Out (And Let Me Cry)"                                
    ##  [31] "19 Somethin'"                                            
    ##  [32] "My Dad"                                                  
    ##  [33] "You Make Me Feel..."                                     
    ##  [34] "My Eyes Get Blurry"                                      
    ##  [35] "Diamonds"                                                
    ##  [36] "Save Me"                                                 
    ##  [37] "R.I.P."                                                  
    ##  [38] "Evol-Not Love"                                           
    ##  [39] "I Have A Dream"                                          
    ##  [40] "Why Do I Love You So"                                    
    ##  [41] "Always"                                                  
    ##  [42] "Body And Soul"                                           
    ##  [43] "You're Breaking My Heart"                                
    ##  [44] "Come With Me"                                            
    ##  [45] "Rock And Roll All Nite"                                  
    ##  [46] "Soul Train"                                              
    ##  [47] "It's A Beautiful Day (For Lovin')"                       
    ##  [48] "What's Wrong With Them"                                  
    ##  [49] "Next Door To The Blues"                                  
    ##  [50] "Life"                                                    
    ##  [51] "White Silver Sands"                                      
    ##  [52] "The Green Door"                                          
    ##  [53] "You Gotta Be"                                            
    ##  [54] "La La La"                                                
    ##  [55] "Do What You Wanna Do"                                    
    ##  [56] "Where I Come From"                                       
    ##  [57] "Baby"                                                    
    ##  [58] "Ghostbusters"                                            
    ##  [59] "Blue Flame"                                              
    ##  [60] "Bibbidi Bobbidi Boo"                                     
    ##  [61] "(You Can Still) Rock In America"                         
    ##  [62] "Happy Ending"                                            
    ##  [63] "Don't Cry For Me Argentina"                              
    ##  [64] "Mental Picture"                                          
    ##  [65] "Oh Honey"                                                
    ##  [66] "I'm Gonna Make You Love Me"                              
    ##  [67] "It's Been Awhile"                                        
    ##  [68] "Mutual Surrender"                                        
    ##  [69] "Summer And Sandy"                                        
    ##  [70] "All Falls Down"                                          
    ##  [71] "Pop Goes The Weasel"                                     
    ##  [72] "Watch Me"                                                
    ##  [73] "Yeah, Yeah, Yeah"                                        
    ##  [74] "Better By The Pound"                                     
    ##  [75] "Glad You Came"                                           
    ##  [76] "When Will It End"                                        
    ##  [77] "Sweet Emotion"                                           
    ##  [78] "Obscene Phone Caller"                                    
    ##  [79] "Absent Minded Me"                                        
    ##  [80] "I Get So Lonely (Oh Baby Mine)"                          
    ##  [81] "Viva Las Vegas"                                          
    ##  [82] "Break It Up"                                             
    ##  [83] "Caught Out There"                                        
    ##  [84] "Every Little Kiss"                                       
    ##  [85] "Check It Out"                                            
    ##  [86] "Last Night I Made A Little Girl Cry"                     
    ##  [87] "Rock Me On The Water"                                    
    ##  [88] "Jenny From The Blosk"                                    
    ##  [89] "Something"                                               
    ##  [90] "The Way Of Love"                                         
    ##  [91] "Temple Of Love"                                          
    ##  [92] "Goodbye To Rome (Arrivederci Roma)"                      
    ##  [93] "All The Way"                                             
    ##  [94] "The Boomin' System"                                      
    ##  [95] "It Must Be Love"                                         
    ##  [96] "Zip Code"                                                
    ##  [97] "Street Singer"                                           
    ##  [98] "She's Like The Wind"                                     
    ##  [99] "Rhythm Of Love"                                          
    ## [100] "Love Won't Let Me Wait"                                  
    ## [101] "Super Highway"                                           
    ## [102] "I Heard It Through The Grapevine"                        
    ## [103] "42196"                                                   
    ## [104] "Be My Baby"                                              
    ## [105] "A Penny A Kiss, A Penny A Hug"                           
    ## [106] "One Sunny Day"                                           
    ## [107] "Rock And Roll"                                           
    ## [108] "Rescue Me"                                               
    ## [109] "Am I Dreaming"                                           
    ## [110] "A Time To Love A Time To Cry"                            
    ## [111] "Kissin' Cousins"                                         
    ## [112] "Another One Bites The Dust"                              
    ## [113] "I Should Cheat On You"                                   
    ## [114] "Song On The Radio"                                       
    ## [115] "My Town My Guy And Me"                                   
    ## [116] "Mambo No. 5"                                             
    ## [117] "I'm Sorry / Calypso"                                     
    ## [118] "My Ballooon's Going Up"                                  
    ## [119] "Hear The Bells"                                          
    ## [120] "Agnes English"                                           
    ## [121] "You Were Made For Me"                                    
    ## [122] "The Beatles Movie Medley"                                
    ## [123] "(Wish I Could Fly Like) Superman"                        
    ## [124] "Fish"                                                    
    ## [125] "Somebody's Knockin'"                                     
    ## [126] "Shut Up + Dance"                                         
    ## [127] "This Is It"                                              
    ## [128] "Let Me Tell You, Babe"                                   
    ## [129] "Tears, Tears, Tears"                                     
    ## [130] "Someday You'll Want Me To Want You"                      
    ## [131] "Two Hearts"                                              
    ## [132] "The Freeze"                                              
    ## [133] "The Bird Man"                                            
    ## [134] "Gone Movin' On"                                          
    ## [135] "Achy Breaky 2"                                           
    ## [136] "Welcome To Atlanta"                                      
    ## [137] "Dance With A Dolly (With A Hole In Her Stocking)"        
    ## [138] "So Sad (To Watch Good Love Go Bad)"                      
    ## [139] "I Like"                                                  
    ## [140] "Jet"                                                     
    ## [141] "The Boys Of Summer"                                      
    ## [142] "Give In To Me"                                           
    ## [143] "Your Other Love"                                         
    ## [144] "Everyday Livin' Days"                                    
    ## [145] "Handsome And Wealthy"                                    
    ## [146] "Time After Time"                                         
    ## [147] "Grits'n Corn Bread"                                      
    ## [148] "You Decorated My Life"                                   
    ## [149] "Devils And Dust"                                         
    ## [150] "One Hit (To The Body)"                                   
    ## [151] "Someone Is Watching"                                     
    ## [152] "Portuguese Washerwoman"                                  
    ## [153] "The Harem"                                               
    ## [154] "Around My Way (Freedom Ain't"                            
    ## [155] "It Keeps Rainin'"                                        
    ## [156] "Vision Of Love"                                          
    ## [157] "What Do Ya Think About That"                             
    ## [158] "Por Favor"                                               
    ## [159] "(You're) Having My Baby"                                 
    ## [160] "Stuntin' Like My Daddy"                                  
    ## [161] "I Want To Love You For What You Are"                     
    ## [162] "One"                                                     
    ## [163] "I Can't Stand The Rain"                                  
    ## [164] "Chariot Rock"                                            
    ## [165] "To Love Somebody"                                        
    ## [166] "You're Good For Me"                                      
    ## [167] "Pop That Thang"                                          
    ## [168] "We Like To Party"                                        
    ## [169] "Paradise"                                                
    ## [170] "Rockin' Red Wing"                                        
    ## [171] "Without You (There Is Nothing)"                          
    ## [172] "C'mon Marianne"                                          
    ## [173] "Don't Talk To Strangers"                                 
    ## [174] "You Make Me Sick"                                        
    ## [175] "Oh Father"                                               
    ## [176] "F.U.R.B."                                                
    ## [177] "I Wish I Could Cry"                                      
    ## [178] "Title"                                                   
    ## [179] "In My Daughter's Eyes"                                   
    ## [180] "Don't Pull Your Love"                                    
    ## [181] "Remember The Name"                                       
    ## [182] "History Repeats Itself"                                  
    ## [183] "State Of Grace"                                          
    ## [184] "Just Be Good To Me"                                      
    ## [185] "The Witch Queen Of New Orleans"                          
    ## [186] "Cha-Hua-Hua"                                             
    ## [187] "You Can't Deny It"                                       
    ## [188] "She Understands Me"                                      
    ## [189] "Concrete Angel"                                          
    ## [190] "Mae"                                                     
    ## [191] "Ready Teddy"                                             
    ## [192] "Two Of A Kind"                                           
    ## [193] "Starlight Starbright"                                    
    ## [194] "Once You Understand"                                     
    ## [195] "7 Things"                                                
    ## [196] "Gangsta"                                                 
    ## [197] "The Philly Freeze"                                       
    ## [198] "Sit With The Guru"                                       
    ## [199] "Door Number Three"                                       
    ## [200] "IfULeave"

## Analysis

You are encouraged to explore these data as you wish using functions
from the packages for the three special variable types. Some ideas that
you might be interested in:

-   What 10 songs (display title, artist, and week) were on the charts
    for the longest?
-   What distinct date did the oldest song(s) leave the charts?
-   What songs could have been played at your 16th birthday party? That
    is, which songs that eventually peaked at \#1 **entered** the charts
    within a couple months (before or after) your 16th birthday?
    Assuming you were 16 years old by 2015.
-   Which artist has been **featured** on the most Billboard charting
    songs?
-   Which artist has **collaborated** on the most Billboard charting
    songs?
-   Create some data visualization controlling the order of the
    character/string variables.

``` r
smol_billboard %>%
  # group_by(`weeks on chart`) %>%
  # arrange(desc(by = `weeks on chart`)) %>%
  # head()
  slice_max(`weeks on chart`, n=10)
```

    ## # A tibble: 11 x 5
    ##    title            artist          `overall peak` `weeks on chart` `chart date`
    ##    <chr>            <chr>                    <dbl>            <dbl>        <dbl>
    ##  1 It's Been Awhile STAIND                       5               46     20020223
    ##  2 You Gotta Be     DES'REE                      5               44     19950701
    ##  3 Glad You Came    THE WANTED                   3               37     20121006
    ##  4 You Make Me Fee… COBRA STARSHIP…              7               29     20120211
    ##  5 The Green Door   JIM LOWE                     1               26     19570306
    ##  6 Somebody's Knoc… TERRI GIBBS                 13               25     19810613
    ##  7 This Is It       KENNY LOGGINS               11               23     19800322
    ##  8 Vision Of Love   MARIAH CAREY                 1               22     19901027
    ##  9 I Can't Stand T… ERUPTION                    18               22     19780805
    ## 10 I Get So Lonely… THE FOUR KNIGH…              3               21     19540618
    ## 11 Don't Talk To S… RICK SPRINGFIE…              2               21     19820724

``` r
smol_billboard %>%
 mutate(chart_date = ymd(`chart date`), leave_chart = `weeks on chart` * 7, y = as.Date(chart_date + leave_chart)) %>%
  slice_min(chart_date) 
```

    ## # A tibble: 1 x 8
    ##   title   artist         `overall peak` `weeks on chart` `chart date` chart_date
    ##   <chr>   <chr>                   <dbl>            <dbl>        <dbl> <date>    
    ## 1 Blue F… WOODY HERMAN …              5                3     19410419 1941-04-19
    ## # … with 2 more variables: leave_chart <dbl>, y <date>

``` r
Nick_birthday <- ymd("19960715")

billboard_songs %>%
  mutate(chart_date = ymd(`chart date`))%>%
  filter(year(chart_date) == 2012)
```

    ## # A tibble: 375 x 6
    ##    title    artist       `overall peak` `weeks on chart` `chart date` chart_date
    ##    <chr>    <chr>                 <dbl>            <dbl>        <dbl> <date>    
    ##  1 Stupid … CASSADEE PO…             40                1     20121229 2012-12-29
    ##  2 Let It … TERRY McDER…             70                1     20121229 2012-12-29
    ##  3 Dance F… BEYONCE                  78               15     20121229 2012-12-29
    ##  4 My Life  50 CENT fea…             27                3     20121229 2012-12-29
    ##  5 Finally… ENRIQUE IGL…             24               14     20121229 2012-12-29
    ##  6 Everybo… NEON TREES                6               39     20121222 2012-12-22
    ##  7 Good Ti… OWL CITY & …              8               24     20121222 2012-12-22
    ##  8 Pop That FRENCH MONT…             36               22     20121222 2012-12-22
    ##  9 I Want … TERRY McDER…             84                1     20121222 2012-12-22
    ## 10 Let It … WIZ KHALIFA…             87                1     20121222 2012-12-22
    ## # … with 365 more rows

## Attribution

Parts of this Activity are based on a lab from [Dr. Kelly
Bodwin’s](https://www.kelly-bodwin.com/) STAT 331 course.
