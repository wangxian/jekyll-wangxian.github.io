---

layout: post
title: "Hello World"
comments: true
category: "其他"

---

第一篇文章，必须是 Hello World !\\
和学一门开发语言一样，一如既往。


**Style h1 ~ h6**

# Big title (h1)

## Middle title (h2)

### Smaller title (h3)

#### and so on (h4)

##### and so on (h5)

###### and so on (h6)


~~~ ruby
def what?
  450
end
~~~

~~~ php
<?php
$valeurs = range(1, 40);
$proba = array_fill(1, 40, 0);
for ($i = 0; $i < 10000; ++$i)
{
    $tirage_tab = array_rand($valeurs, 10);
    foreach($tirage_tab as $key => $value)
    {
        $proba[$valeurs[$value]]++;
    }
}

asort($proba);
echo "Proba : <br/>\n";
foreach($proba as $key => $value)
{
    echo "$key : $value<br/>\n";
}
?>
~~~