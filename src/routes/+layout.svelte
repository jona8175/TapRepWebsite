<!-- Hier wird das menu erstelt was wir across all pages benutzen, 
 an dieser stelle könnten ähnlich dinge gemacht werden-->

<nav>
  <ul>
    <li><a href="/">Welcome</a></li>
    <li><a href="/blockdiagram">Blockdiagram</a></li>
    <li><a href="#">Orte</a></li>
    <li><a href="#">Über uns</a></li>
    <li><a href="/help">hilfe</a></li>
  </ul>
</nav>

<!-- im slot ist der inhalt der sub-page-->
<div>
  <slot></slot>
</div>


<style>
/* Menu stuff*/

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float: left;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover {
  background-color: #111;
}

/* Text pages*/
.sheet {
  background-color: rgb(230, 236, 236);
  padding-right: 70pt;
  padding-left: 50pt;
  padding-bottom: 100pt;
  margin-top: 0px;
  margin-bottom: 0px;
  margin-right: 50px;
  margin-left: 50px;
  display: flex;
  flex-direction: column;
}
</style>

<script>
  let scene =1;
</script>