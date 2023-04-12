<template>
  <div>
    <NavBar :logo="logo_src" :alt="app_name" />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import Footer from "./components/Footer.vue";
export default {
  components: {
    NavBar,
    Footer,
  },
  data() {
    return {
      logo_src: "./img/logo.png",
      app_name: "Make your churros",
    };
  },
};
</script>

<style>
/* http://meyerweb.com/eric/tools/css/reset/
   v2.0 | 20110126
   License: none (public domain)
  */

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  font-family: "Poppins", sans-serif;
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;700&display=swap");

:root {
  --fonte: "Poppins", sans-serif;
  --azul-escuro: #13222f;

  --amarelo: #f2c166;

  --laranja: #f28d52;

  --bege: #d9b19a;

  --marrom-vermelhado: #733119;

  --preto: #03080c;
  --branco: #f7efea;
}

body {
  font-family: var(--fonte);
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: var(--preto);
}
</style>
