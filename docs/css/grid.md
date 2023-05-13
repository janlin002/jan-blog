# Grid

## 什麼是 Grid？
`grid` 是 css 中的一種排版方式，常常會拿來跟 `flex` 作比較，他們兩個不同的點在於: `flex` 是一維的，而 `grid` 是二維的

## Grid 怎麼使用？

透過設定欄（column) 列 (row) 來達成排版的功能。
可分為包裹的容器（container) 與被包裹的項目（item)，有各自的屬性可設置

![img](https://i0.wp.com/yukihiew.com/wp-content/uploads/2021/08/600x400-1.png?w=600&ssl=1)

### container

container 是包裹在最外層的容器(外層才會有 `template`)

```css
.container{ 
    display: grid | inline-grid | subgrid; 
        // 縱向排列 | 橫向排列 | 是item也是container
    grid-template: 5px 40px auto 40px 5px / 40px 25% 2fr fr; 
        // 列(row)線的間距 / 欄(column)線的間距
    
    -也可個別設定row、column(通常這也寫比較好，可讀性較高)
    grid-template-rows: 5px 40px auto 40px 5px;
    grid-template-columns: 40px 25% 2fr fr;

    -線是可以命名的，名字加在數值前
    grid-template-rows: [line1]40px [second-line]25% [3line]2fr [forth-line]fr;

    -也可使用repeat(數量, 寬度[名字]) 作設定
    grid-template-columns: repeat(3, 40px[colline]);
    等同於 grid-template-columns: [colline]40px [colline]40px [colline]40px;
}
```

### item

item 就是內部屬性

item可分為:
- 用線(line)設定範圍
- 用區塊(area)做分配

#### 用線(line)設定範圍

```css
.item{
-item要佔據的範圍
grid-area: 1 / 3 / 3 / 4 ; 
//row-start / column-start / row-end / column-end

-也可分別寫
grid-row: 1 / 3 ; // startline / endline
grid-column: 3 / 4 ; // startline / endline

-如果只寫2，代表2-3的單位
grid-row: 2; 
== grid-row: 2 / 3;

-開始線和結束線也可分開寫
grid-row-start: 1 ;
grid-row-end: 3 ;
grid-column-start: 3 ; 
grid-column-end: 4 ;
}

-若有多條同名線，在item使用可在名字後方加上數字做為index，這邊的 colline 就是剛剛的 [colline]
grid-column-start: colline 2; //第二條叫做colline的線

-單位前皆可加上span表示擴展一條線的距離，
grid-column: span 2 / span 6 ; // 1<-2 / 6->7
== grid-column: 1 / 7;
```

#### 用區塊(area)作分配

須先在 container 定義好空間

```css
-設定item的區塊名稱
.item1{ grid-area: header; } 
.item2{ grid-area: main; }
.item3{ grid-area: footer; }
.item4{ grid-area: sidebar; }

-再透過container排版
grid-template-areas: 
"header header header header"
"main main main sidebar"
"main main main sidebar"
"footer footer footer footer"

-另外還有"none" ，"."兩個值，"none"是沒有指定區塊，"."是代表空格。
-item的分配不能是分段的，也不能是非四方形。
```

### gap

grid有調整間隔的屬性

#### 間隔

```css
.container
grid-gap: 5px 10px; //row的間隔 column的間隔
-可分開寫
grid-row-gap: 5px;
grid-column-gap: 10px;
```

#### 對齊

```csss
```

### 參考文章

[強大的CSS grid網格排版-介紹與應用](https://yukihiew.com/about-css-grid/)

[CSS Grid 屬性介紹](https://www.casper.tw/css/2017/03/22/css-grid-layout/)

[Day 6 : HTML - 網頁排版超強神器part_2，CSS grid到底是什麼？](https://ithelp.ithome.com.tw/m/articles/10268087)