---
title: "loops y funciones md"
author: "Nicolas"
date: "27/8/2021"
output: 
  html_document: 
    keep_md: yes
---



```r
rm(list = ls())
library("tidyverse")
```

```
## Warning: package 'tidyverse' was built under R version 4.0.5
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.1.2     v dplyr   1.0.6
## v tidyr   1.1.3     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.1
```

```
## Warning: package 'tibble' was built under R version 4.0.5
```

```
## Warning: package 'tidyr' was built under R version 4.0.5
```

```
## Warning: package 'dplyr' was built under R version 4.0.5
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
set.seed(1244)

palabras <- words
palabras
```

```
##   [1] "a"           "able"        "about"       "absolute"    "accept"     
##   [6] "account"     "achieve"     "across"      "act"         "active"     
##  [11] "actual"      "add"         "address"     "admit"       "advertise"  
##  [16] "affect"      "afford"      "after"       "afternoon"   "again"      
##  [21] "against"     "age"         "agent"       "ago"         "agree"      
##  [26] "air"         "all"         "allow"       "almost"      "along"      
##  [31] "already"     "alright"     "also"        "although"    "always"     
##  [36] "america"     "amount"      "and"         "another"     "answer"     
##  [41] "any"         "apart"       "apparent"    "appear"      "apply"      
##  [46] "appoint"     "approach"    "appropriate" "area"        "argue"      
##  [51] "arm"         "around"      "arrange"     "art"         "as"         
##  [56] "ask"         "associate"   "assume"      "at"          "attend"     
##  [61] "authority"   "available"   "aware"       "away"        "awful"      
##  [66] "baby"        "back"        "bad"         "bag"         "balance"    
##  [71] "ball"        "bank"        "bar"         "base"        "basis"      
##  [76] "be"          "bear"        "beat"        "beauty"      "because"    
##  [81] "become"      "bed"         "before"      "begin"       "behind"     
##  [86] "believe"     "benefit"     "best"        "bet"         "between"    
##  [91] "big"         "bill"        "birth"       "bit"         "black"      
##  [96] "bloke"       "blood"       "blow"        "blue"        "board"      
## [101] "boat"        "body"        "book"        "both"        "bother"     
## [106] "bottle"      "bottom"      "box"         "boy"         "break"      
## [111] "brief"       "brilliant"   "bring"       "britain"     "brother"    
## [116] "budget"      "build"       "bus"         "business"    "busy"       
## [121] "but"         "buy"         "by"          "cake"        "call"       
## [126] "can"         "car"         "card"        "care"        "carry"      
## [131] "case"        "cat"         "catch"       "cause"       "cent"       
## [136] "centre"      "certain"     "chair"       "chairman"    "chance"     
## [141] "change"      "chap"        "character"   "charge"      "cheap"      
## [146] "check"       "child"       "choice"      "choose"      "Christ"     
## [151] "Christmas"   "church"      "city"        "claim"       "class"      
## [156] "clean"       "clear"       "client"      "clock"       "close"      
## [161] "closes"      "clothe"      "club"        "coffee"      "cold"       
## [166] "colleague"   "collect"     "college"     "colour"      "come"       
## [171] "comment"     "commit"      "committee"   "common"      "community"  
## [176] "company"     "compare"     "complete"    "compute"     "concern"    
## [181] "condition"   "confer"      "consider"    "consult"     "contact"    
## [186] "continue"    "contract"    "control"     "converse"    "cook"       
## [191] "copy"        "corner"      "correct"     "cost"        "could"      
## [196] "council"     "count"       "country"     "county"      "couple"     
## [201] "course"      "court"       "cover"       "create"      "cross"      
## [206] "cup"         "current"     "cut"         "dad"         "danger"     
## [211] "date"        "day"         "dead"        "deal"        "dear"       
## [216] "debate"      "decide"      "decision"    "deep"        "definite"   
## [221] "degree"      "department"  "depend"      "describe"    "design"     
## [226] "detail"      "develop"     "die"         "difference"  "difficult"  
## [231] "dinner"      "direct"      "discuss"     "district"    "divide"     
## [236] "do"          "doctor"      "document"    "dog"         "door"       
## [241] "double"      "doubt"       "down"        "draw"        "dress"      
## [246] "drink"       "drive"       "drop"        "dry"         "due"        
## [251] "during"      "each"        "early"       "east"        "easy"       
## [256] "eat"         "economy"     "educate"     "effect"      "egg"        
## [261] "eight"       "either"      "elect"       "electric"    "eleven"     
## [266] "else"        "employ"      "encourage"   "end"         "engine"     
## [271] "english"     "enjoy"       "enough"      "enter"       "environment"
## [276] "equal"       "especial"    "europe"      "even"        "evening"    
## [281] "ever"        "every"       "evidence"    "exact"       "example"    
## [286] "except"      "excuse"      "exercise"    "exist"       "expect"     
## [291] "expense"     "experience"  "explain"     "express"     "extra"      
## [296] "eye"         "face"        "fact"        "fair"        "fall"       
## [301] "family"      "far"         "farm"        "fast"        "father"     
## [306] "favour"      "feed"        "feel"        "few"         "field"      
## [311] "fight"       "figure"      "file"        "fill"        "film"       
## [316] "final"       "finance"     "find"        "fine"        "finish"     
## [321] "fire"        "first"       "fish"        "fit"         "five"       
## [326] "flat"        "floor"       "fly"         "follow"      "food"       
## [331] "foot"        "for"         "force"       "forget"      "form"       
## [336] "fortune"     "forward"     "four"        "france"      "free"       
## [341] "friday"      "friend"      "from"        "front"       "full"       
## [346] "fun"         "function"    "fund"        "further"     "future"     
## [351] "game"        "garden"      "gas"         "general"     "germany"    
## [356] "get"         "girl"        "give"        "glass"       "go"         
## [361] "god"         "good"        "goodbye"     "govern"      "grand"      
## [366] "grant"       "great"       "green"       "ground"      "group"      
## [371] "grow"        "guess"       "guy"         "hair"        "half"       
## [376] "hall"        "hand"        "hang"        "happen"      "happy"      
## [381] "hard"        "hate"        "have"        "he"          "head"       
## [386] "health"      "hear"        "heart"       "heat"        "heavy"      
## [391] "hell"        "help"        "here"        "high"        "history"    
## [396] "hit"         "hold"        "holiday"     "home"        "honest"     
## [401] "hope"        "horse"       "hospital"    "hot"         "hour"       
## [406] "house"       "how"         "however"     "hullo"       "hundred"    
## [411] "husband"     "idea"        "identify"    "if"          "imagine"    
## [416] "important"   "improve"     "in"          "include"     "income"     
## [421] "increase"    "indeed"      "individual"  "industry"    "inform"     
## [426] "inside"      "instead"     "insure"      "interest"    "into"       
## [431] "introduce"   "invest"      "involve"     "issue"       "it"         
## [436] "item"        "jesus"       "job"         "join"        "judge"      
## [441] "jump"        "just"        "keep"        "key"         "kid"        
## [446] "kill"        "kind"        "king"        "kitchen"     "knock"      
## [451] "know"        "labour"      "lad"         "lady"        "land"       
## [456] "language"    "large"       "last"        "late"        "laugh"      
## [461] "law"         "lay"         "lead"        "learn"       "leave"      
## [466] "left"        "leg"         "less"        "let"         "letter"     
## [471] "level"       "lie"         "life"        "light"       "like"       
## [476] "likely"      "limit"       "line"        "link"        "list"       
## [481] "listen"      "little"      "live"        "load"        "local"      
## [486] "lock"        "london"      "long"        "look"        "lord"       
## [491] "lose"        "lot"         "love"        "low"         "luck"       
## [496] "lunch"       "machine"     "main"        "major"       "make"       
## [501] "man"         "manage"      "many"        "mark"        "market"     
## [506] "marry"       "match"       "matter"      "may"         "maybe"      
## [511] "mean"        "meaning"     "measure"     "meet"        "member"     
## [516] "mention"     "middle"      "might"       "mile"        "milk"       
## [521] "million"     "mind"        "minister"    "minus"       "minute"     
## [526] "miss"        "mister"      "moment"      "monday"      "money"      
## [531] "month"       "more"        "morning"     "most"        "mother"     
## [536] "motion"      "move"        "mrs"         "much"        "music"      
## [541] "must"        "name"        "nation"      "nature"      "near"       
## [546] "necessary"   "need"        "never"       "new"         "news"       
## [551] "next"        "nice"        "night"       "nine"        "no"         
## [556] "non"         "none"        "normal"      "north"       "not"        
## [561] "note"        "notice"      "now"         "number"      "obvious"    
## [566] "occasion"    "odd"         "of"          "off"         "offer"      
## [571] "office"      "often"       "okay"        "old"         "on"         
## [576] "once"        "one"         "only"        "open"        "operate"    
## [581] "opportunity" "oppose"      "or"          "order"       "organize"   
## [586] "original"    "other"       "otherwise"   "ought"       "out"        
## [591] "over"        "own"         "pack"        "page"        "paint"      
## [596] "pair"        "paper"       "paragraph"   "pardon"      "parent"     
## [601] "park"        "part"        "particular"  "party"       "pass"       
## [606] "past"        "pay"         "pence"       "pension"     "people"     
## [611] "per"         "percent"     "perfect"     "perhaps"     "period"     
## [616] "person"      "photograph"  "pick"        "picture"     "piece"      
## [621] "place"       "plan"        "play"        "please"      "plus"       
## [626] "point"       "police"      "policy"      "politic"     "poor"       
## [631] "position"    "positive"    "possible"    "post"        "pound"      
## [636] "power"       "practise"    "prepare"     "present"     "press"      
## [641] "pressure"    "presume"     "pretty"      "previous"    "price"      
## [646] "print"       "private"     "probable"    "problem"     "proceed"    
## [651] "process"     "produce"     "product"     "programme"   "project"    
## [656] "proper"      "propose"     "protect"     "provide"     "public"     
## [661] "pull"        "purpose"     "push"        "put"         "quality"    
## [666] "quarter"     "question"    "quick"       "quid"        "quiet"      
## [671] "quite"       "radio"       "rail"        "raise"       "range"      
## [676] "rate"        "rather"      "read"        "ready"       "real"       
## [681] "realise"     "really"      "reason"      "receive"     "recent"     
## [686] "reckon"      "recognize"   "recommend"   "record"      "red"        
## [691] "reduce"      "refer"       "regard"      "region"      "relation"   
## [696] "remember"    "report"      "represent"   "require"     "research"   
## [701] "resource"    "respect"     "responsible" "rest"        "result"     
## [706] "return"      "rid"         "right"       "ring"        "rise"       
## [711] "road"        "role"        "roll"        "room"        "round"      
## [716] "rule"        "run"         "safe"        "sale"        "same"       
## [721] "saturday"    "save"        "say"         "scheme"      "school"     
## [726] "science"     "score"       "scotland"    "seat"        "second"     
## [731] "secretary"   "section"     "secure"      "see"         "seem"       
## [736] "self"        "sell"        "send"        "sense"       "separate"   
## [741] "serious"     "serve"       "service"     "set"         "settle"     
## [746] "seven"       "sex"         "shall"       "share"       "she"        
## [751] "sheet"       "shoe"        "shoot"       "shop"        "short"      
## [756] "should"      "show"        "shut"        "sick"        "side"       
## [761] "sign"        "similar"     "simple"      "since"       "sing"       
## [766] "single"      "sir"         "sister"      "sit"         "site"       
## [771] "situate"     "six"         "size"        "sleep"       "slight"     
## [776] "slow"        "small"       "smoke"       "so"          "social"     
## [781] "society"     "some"        "son"         "soon"        "sorry"      
## [786] "sort"        "sound"       "south"       "space"       "speak"      
## [791] "special"     "specific"    "speed"       "spell"       "spend"      
## [796] "square"      "staff"       "stage"       "stairs"      "stand"      
## [801] "standard"    "start"       "state"       "station"     "stay"       
## [806] "step"        "stick"       "still"       "stop"        "story"      
## [811] "straight"    "strategy"    "street"      "strike"      "strong"     
## [816] "structure"   "student"     "study"       "stuff"       "stupid"     
## [821] "subject"     "succeed"     "such"        "sudden"      "suggest"    
## [826] "suit"        "summer"      "sun"         "sunday"      "supply"     
## [831] "support"     "suppose"     "sure"        "surprise"    "switch"     
## [836] "system"      "table"       "take"        "talk"        "tape"       
## [841] "tax"         "tea"         "teach"       "team"        "telephone"  
## [846] "television"  "tell"        "ten"         "tend"        "term"       
## [851] "terrible"    "test"        "than"        "thank"       "the"        
## [856] "then"        "there"       "therefore"   "they"        "thing"      
## [861] "think"       "thirteen"    "thirty"      "this"        "thou"       
## [866] "though"      "thousand"    "three"       "through"     "throw"      
## [871] "thursday"    "tie"         "time"        "to"          "today"      
## [876] "together"    "tomorrow"    "tonight"     "too"         "top"        
## [881] "total"       "touch"       "toward"      "town"        "trade"      
## [886] "traffic"     "train"       "transport"   "travel"      "treat"      
## [891] "tree"        "trouble"     "true"        "trust"       "try"        
## [896] "tuesday"     "turn"        "twelve"      "twenty"      "two"        
## [901] "type"        "under"       "understand"  "union"       "unit"       
## [906] "unite"       "university"  "unless"      "until"       "up"         
## [911] "upon"        "use"         "usual"       "value"       "various"    
## [916] "very"        "video"       "view"        "village"     "visit"      
## [921] "vote"        "wage"        "wait"        "walk"        "wall"       
## [926] "want"        "war"         "warm"        "wash"        "waste"      
## [931] "watch"       "water"       "way"         "we"          "wear"       
## [936] "wednesday"   "wee"         "week"        "weigh"       "welcome"    
## [941] "well"        "west"        "what"        "when"        "where"      
## [946] "whether"     "which"       "while"       "white"       "who"        
## [951] "whole"       "why"         "wide"        "wife"        "will"       
## [956] "win"         "wind"        "window"      "wish"        "with"       
## [961] "within"      "without"     "woman"       "wonder"      "wood"       
## [966] "word"        "work"        "world"       "worry"       "worse"      
## [971] "worth"       "would"       "write"       "wrong"       "year"       
## [976] "yes"         "yesterday"   "yet"         "you"         "young"
```

```r
length(palabras)
```

```
## [1] 980
```

```r
palabras3 <- sample(words, 200)

tamaño <- c()

for (i in seq_along(palabras)){
  tamaño[i] <- nchar(palabras[i])
}
length(tamaño)
```

```
## [1] 980
```

```r
tamaño[1:10]
```

```
##  [1] 1 4 5 8 6 7 7 6 3 6
```

```r
palabras[1:10]
```

```
##  [1] "a"        "able"     "about"    "absolute" "accept"   "account" 
##  [7] "achieve"  "across"   "act"      "active"
```

Luego creamos la función de contar letras:

```r
contar_letras <- function(x){
tamaño <<- c()
for (i in seq_along(x)){
 tamaño[i] <<- nchar(x[i])
} 
  }
contar_letras(palabras)
summary(tamaño)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   1.000   4.000   5.000   5.231   6.000  11.000
```
Listas

Ejemplos

```r
saber11_2019 <- read_delim("C:/Users/Nicolas/OneDrive - Universidad Externado de Colombia/8vo Semestre/z,Monitoria Fun.programacion/Scripts/saber11_2019.csv", 
 ";", escape_double = FALSE, trim_ws = TRUE)
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_character(),
##   PERIODO = col_double(),
##   COLE_COD_DANE_ESTABLECIMIENTO = col_double(),
##   COLE_COD_DANE_SEDE = col_double(),
##   PUNT_LECTURA_CRITICA = col_double(),
##   PERCENTIL_LECTURA_CRITICA = col_double(),
##   DESEMP_LECTURA_CRITICA = col_double(),
##   PUNT_MATEMATICAS = col_double(),
##   PERCENTIL_MATEMATICAS = col_double(),
##   DESEMP_MATEMATICAS = col_double(),
##   PUNT_C_NATURALES = col_double(),
##   PERCENTIL_C_NATURALES = col_double(),
##   DESEMP_C_NATURALES = col_double(),
##   PUNT_SOCIALES_CIUDADANAS = col_double(),
##   PERCENTIL_SOCIALES_CIUDADANAS = col_double(),
##   DESEMP_SOCIALES_CIUDADANAS = col_double(),
##   PUNT_INGLES = col_double(),
##   PERCENTIL_INGLES = col_double(),
##   PUNT_GLOBAL = col_double(),
##   PERCENTIL_GLOBAL = col_double(),
##   ESTU_INSE_INDIVIDUAL = col_double()
##   # ... with 2 more columns
## )
## i Use `spec()` for the full column specifications.
```

```r
puntajes <- saber11_2019 %>% select(starts_with("PUNT"))
#puntajes <- select(saber11_2019, starts_with("PUNT"))
```
mapply
Aplica una función a los primeros elementos de cada argumento, a los segundos, a los terceros, y así sucesivamente. Los argumentos se reciclan si es necesario.

```r
str(mapply)
```

```
## function (FUN, ..., MoreArgs = NULL, SIMPLIFY = TRUE, USE.NAMES = TRUE)
```
Ejemplo 1

```r
mapply(function(x,y){x^y},x=c(2,3),y=c(3,4))
```

```
## [1]  8 81
```

Aplica la función definida por el usuario, aplicando el argumento de la segunda variable al argumento de la
primera variable.

Ejemplo 2

Supongamos que tenemos tres de vectores:


```r
values1 <- list(a = c(1, 2, 3), b = c(13, 14, 15), c = c(27, 28))
values2 <- list(d = c(10, 11, 12), e = c(13, 14, 15), f = c(16, 17, 18))
values3 <- list(g = c(2, 4, 6, 8), h = c(11, 14, 16, 18), j = c(23, 25, 27, 21))
```

Observe que cada lista tiene el mismo número de elementos (tres), pero no son necesariamente de la misma
longitud.

A cada lista se le puede calcular el máximo:

```r
t(lapply(values1, max))
```

```
##      a b  c 
## [1,] 3 15 28
```

```r
t(lapply(values2, max))
```

```
##      d  e  f 
## [1,] 12 15 18
```


```r
t(lapply(values3, max))
```

```
##      g h  j 
## [1,] 8 18 27
```

Se puede unir para observarlo mejor:

```r
cbind(lapply(values1, max), lapply(values2, max), lapply(values3, max))
```

```
##   [,1] [,2] [,3]
## a 3    12   8   
## b 15   15   18  
## c 28   18   27
```

Pero queremos obtener el valor máximo para cada trío. Para ello es útil la función mapply:


```r
mapply(function(num1, num2, num3) max(c(num1, num2, num3)), values1, values2, values3)
```

```
##  a  b  c 
## 12 18 28
```

Para verificar, se puede unir para observar cómo es el máximo de cada trío de valores:

```r
cbind(lapply(values1, max), lapply(values2, max), lapply(values3, max), mapply(function(num1, num2, num3) max(c(num1, num2, num3)), values1, values2, values3))
```

```
##   [,1] [,2] [,3] [,4]
## a 3    12   8    12  
## b 15   15   18   18  
## c 28   18   27   28
```

tapply
Aplica la función sobre subgrupos identificados mediante una variable tipo factor

```r
Edad <- c(rnorm(20, 10, 3), runif(20, 18, 62))
Grupo <- gl(2, k = 20, labels = c('Niños', 'Adultos'))
tapply(Edad, Grupo, min)
```

```
##     Niños   Adultos 
##  6.279525 18.632838
```


```r
tapply(Edad, Grupo, max)
```

```
##    Niños  Adultos 
## 16.80505 61.28019
```

