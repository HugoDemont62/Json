# Json




## Data Management

## with


## JSON files and PHP



---


## I. Introduction


### 1. Presentation of the problem

During different searches on the internet, I realized that very little information is on the subject of reading information since a JSON file for websites.


### 2. Objectivity

In the document you will find how to use the information correctly thanks to some examples. It should be noted that the author of this report seeks to report the findings of the analysis of this research in an objective manner.


### 3. Motivation

The motivations for writing this article are the result of a lack of precise information on the subject of the JSON with some differences between the JSON Objects and the JSON Tables.

---



## II. Exhibition


### 1. Presentation of the topic

To fully understand the explanations, we need to establish some things, I wish with this article to teach you to use the JSON as storage space even if the BDD (Database) in MySQL is much more secure than the JSON folders. Here not to fade in front of a web development topic I show you roughly how JSON works with PHP.

JSON means JavaScript Object Notation JSON. It is a text format for storing and transporting JSON data. It is "self-descriptive" and easy to understand.

We have to have a number of things at our disposal to get into the code.

A code editor (PhpStorm / VSCode / …),

Basic knowledge of PHP,

Have a JSON file(below for my article),

Key 1 and Key 2 images: [1](https://ibb.co/R47RkMH ) and [2](https://ibb.co/hHRHS0m)

And of the motivation!



JSON file:

File name: products.json

```
{
"R230595": { "Title": "SanDisk 32G USB Key",
"imageUrl": "clef1.jpg",
"description": "32 GB, USB 3.0 (USB 2.0 compatible)",
"price": 23.99,
"type" : "cle"},
"R250075": { "title": "Emtec Flash Voyager 32",
"imageUrl": "clef2.jpg",
"description": "32 GB, USB 3.0 (USB 2.0 compatible)",
"price": 19.99,
"type" : "cle" }
}
```

---



## III. When we have objects


### 1. Recovery

We are in a php file regardless of its name, we will initially retrieve the information of the JSON file named “products.json”. In PHP two important functions will be useful to decrypt the file JSON.

“fle_get_contents” and “json_decode”, the fle_get_contents() will retrieve the file where we put it. For example, if my file is in a data folder I will do:
file_get_contents('data/products.json');

This little bit of code will look in the data folder for file products.json, enfn we can enter this fle_get_contents into a variable.

The second function "json_decode" will decrypt a json file by using it as an associative array where we have additional information with true or leave them as a JSON object with false, this result can also be stored in a variable.

To take the information we must therefore have a code that looks like this:


`$filename = 'data/products.json';

$arrays = json_decode(file_get_contents($filename),true); var_dump($tables);`



So here it will be in our WAMP server:

```
array (size=2)

'R230595' =>

array (size=5)

'title' => string 'SanDisk 32G' (length=20)

'imageUrl' => string 'clef1.jpg' (length=25)

'description' => string '32 GB, USB 3.0 (USB 2.0 compatible)' (length=35)

'price' => foat 23.99

'type' => string 'cle' (length=3)

'R250075' =>

array (size=5)

'title' => string 'Emtec Flash Voyager 32' (length=22)

'imageUrl' => string 'clef2.jpg' (length=25)

'description' => string '32 GB, USB 3.0 (USB 2.0 compatible)' (length=35)

'price' => foat 19.99

'type' => string 'cle' (length=3)
```


So we get an associative table that will serve us in the next part of the chapter.

Note that we get exactly the same thing as the JSON file , but this time we can use the information from the associative array.

### 2. Display


Certainly we know how to recover the information of a JSON file but for the moment impossible to afcher in the state with a var_dump($tableaux);We want to see the images and information correctly with html and why not css/scss.

In our associative table the keys are the references of the products, like “R230595” and others, we want the different information inside the table for this we need to make a loop to retrieve the information of the tables.

`foreach ($tableau as $key=>$val)`

In the $arrays which is the json_decode we assign two values the key which is $key and the value of the key which is $val.

To afcher the information of a product we must for more ease use a function why not afcheProduit.

Our loop where we want to send the information must therefore correspond to this code:


`foreach ($tableaux as $key=>$val) {`

`Product Display($key);`
`}`

For the function we have to retrieve the $key which is the product reference of the famous “R230595” to use it for taking information in the afchage.

To write html in PHP we will use an echo with quotes to avoid problems with the “” of html.


So we get: `echo ''`; Inside you inject your HTML code.


To obtain the information we must write in the echo the file decrypted the reference and enfn
the information. In a PHP echo to write inside we have to use quotes and dots,
for our information stored in the associative array “arrays” if we wish to
afcher we just have to write the name of the array in which object they are stored and enfn the
Desired key to have the value that is enclosed.
Which gives us:

```
`<img class="produits__image" src="'.$tableaux[$produit]['imageUrl'].'" alt="clé">`
```

Here we have the $tableau which is the associative tableau, the $produit which is the reference of our products and infn the ‘imageUrl’ which is simply the key of the address of the image: 'imageUrl' => string 'clef1.jpg' so we have in the src clef1.jpg which we get our image.

Here is a code for each element:


```
function displayProduct($produit){

$filename = 'data/products.json';
$arrays = json_decode(file_get_contents($filename),true); echo '
<li class="productts__item">
<div class="productts__pic">
<a href=""><img class="produits__image" src="'.$tableaux[$produit]['imageUrl'].'" alt="clé"></a>
</div>
<div class="products__infos">
<a class="productts__name text"
href="article.php? reference='. $produit. '">'. $tableaux[$produit]['titre'
]. ' ('.$produit.')</a>
<p class="products__desc
desc">'. $tableaux[$produit]['description']. '</p>
</div>
<div class="products__cta">
<a class="productts__link"
href="adderPanier.php? reference='. $produit. '"><img
class="productts__addtocart" src="assets/site/buy.png"
alt="buy"></a>
<p class="products__prix
text">'. $tableaux[$produit]['prix']. '€</p> </div>

</li>';

}
```

The classes have been adapted to my css code I let you do it for your css code.

---


## IV. When we have objects and paintings


### 1. Recovery

We have seen and understood how the JSON afchage works in php. But! This is not the only case observed, let’s take a new example! If we have comments to afcher to this kind of product as in the new file JSON that I will give you:




The file JSON avis.json:

```
{
"Comments":[
{"reference": "R230595",
"Author": "Seb",
"date" : "12/05/2018",
"note":7,
"Review": "Great product I recommend"},
{"reference": "R230595",
"author": "Gilles",
"date" : "17/06/2018",
"note":8,
"Review":"Product meets my expectations. Delivery is always at the top!" },
{"reference": "R250075",
"author": "Vincent",
"date" : "05/08/2018",
"note": 4,
"Review": "Good quality product but no instructions from
montage. I had to look online. Bof Bof :-("}
]
}
```




### 2. comprehension

In the new file JSON we have a new specificity, don’t be afraid! it’s quite simple! We have in a defined JSON object with the {} at the beginning up to the fn but inside this set, we have a table delimited with the [] which complicates us a little more the task during the display but nothing serious! We will try to display each comment in relation to the product.



### 3. Code

First of all it is necessary to decode the file again at the entry of the function that we will name afcheCommentaire. So you can reuse the code previously with the modification of the name of the file which gives:

```
`function displayCommentary() {

$filename = 'data/avis.json';
$arrays = json_decode(file_get_contents($filename), true);
}`
```

Enfn we have to use the associative array to fetch the information, as previously we have to use the associative array, for this in your html code in the echo you will use the: '.$arrays['comments']. ' but we have a problem, comment is a table, with IDs, to be able to afcher them we are therefore obliged to make a loop for to take the information. Which gives us overall:

```
`<p class="commentaires__par">by <span

class="text">'. $tables['comments'][$i]['author']. '</span></p>`
```

Here the code afche the author of the comments, but to have the $i we must make a loop for as opposite:

`for ($i = 0; $i < count($tables['comments']); $i++){

}`

In order to have the elements of a particular product, of the comments of the product in question, we are therefore obliged to make an if in this for loop to require that the reference of the product is the same as the $_GET[‘reference’] given when sending to the article. Which gives us a very simple code. I even added a function when there are no comments! The code:





```
function displayCommentary() {

$filename = 'data/avis.json';
$arrays = json_decode(file_get_contents($filename), true);



echo '

<h2 class="text heading">Comments</h2> <div class="commentaires__grid">';
$com = false;

for	($i = 0; $i < count($tables['comments']); $i++){ if ($tables['comments'][$i]['reference'] =

$_GET['reference']){
$com = true;
echo ' ' <div class="commentaires__user">
<p class="commentaires__par">by <span class="text">'. $tables['comments'][$i]['author']. '</span></p>
<p
class="commentaires__posted">'. $tableaux['commentaires'][$i]['date'].
'</p>
<p
class="commentaires__note">'. $tableaux['commentaires'][$i]['note']. '/
10</p>
</div>
<div class="commentaires__avis">
<p
class="commentaires__text">'. $tableaux['commentaires'][$i]['avis']. '< /p>
</div>';

}

}
if (!$com){
echo '<i>No comments</i>';
}
echo '</div>';

}
```

---

### 
V. Conclusion



And yes! it is quite simple to afcher each element but without having any knowledge in PHP or JSON, it is complicated to orient oneself in all this. I hope this article helped you in your code! Other codes are possible such as knowing the number of notices, calculating the average of notices, putting items in a shopping cart, etc. , for the part of the afchage you should succeed by following my “advice”. Good luck!


Sory for my very bad english im just a french guy.



Hugo Demont, étudiant à l’université

LENS technology in the first year of LENS MMI
