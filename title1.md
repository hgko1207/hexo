<h2 style="padding: 0.3em 0.5em; margin: 0.5em 0em; color: #000; border-left: 12px solid #4272D7; border-bottom: 1px #4272D7 solid;" data-ke-size="size26"><b>제목 1</b></h2>

<h3 style="padding: 0em 1.1em 0em 0.5em; margin: 0.5em 0em; color: #000000; border-left: #444444 6px solid; font-weight: bold;" data-ke-size="size23"><b><span style="font-family: AppleSDGothicNeo-Regular, 'Malgun Gothic', '맑은 고딕', dotum, 돋움, sans-serif;">제목 2</span></b></h3>

```css
.book-toc {
  position: relative;
  width: fit-content;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #a68c69;
  background-color: #f9f3e9;
}
.book-toc p {
  font-weight: 700;
  font-size: 1.2em !important;
  color: #8a704c;
  border-bottom: 2px solid #a68c69;
  margin-bottom: 15px;
  padding-bottom: 5px;
}
#toc * {
  font-size: 18px;
  color: #7b6145 !important;
}
#toc {
  padding: 0 20px 0 25px;
}
#toc a:hover {
  color: #a68c69;
}
#toc > li {
  padding-left: 0;
  text-indent: 0;
  list-style-type: none;
  margin-bottom: 10px;
  margin-top: 7px;
  position: relative;
}
#toc > li:before {
  content: '▸';
  position: absolute;
  left: -20px;
  top: 50%;
  transform: translateY(-50%);
  color: #a68c69;
}
#toc > li > a {
  text-decoration: none;
  font-weight: 700;
  border-bottom: 1px dotted #a68c69;
  transition: color 0.3s ease;
}
#toc > li > ul {
  padding-left: 20px;
}
#toc > li > ul > li {
  font-size: 0.87em;
}
#toc > li > ul > li > a {
  font-size: 1em;
  text-decoration: none;
}
#toc > li > ul > li > ul {
  padding-left: 20px;
}
#toc > li > ul > li > ul > li {
  font-size: 0.87em;
}
#toc > li > ul > li > ul > li > a {
  font-size: 0.875em;
  text-decoration: none;
}
```
