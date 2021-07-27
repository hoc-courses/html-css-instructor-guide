# News Site Progressive Project

This is a progression lab that starts with building a static news site at the end of the HTML/CSS portion of the class and progresses through the end of the course with dynamic content coming from both a public API (New York Times) and our MERN back-end.

As an example of the progressive change from a static to dyanmic site, this is how the Article Grid is replaced with dynamic content:
* replace static articles in grid with pulling them from static array of article data.
* build functions to generate the HTML as a string for each of the page components and use the DOM's innerHTML to update the content. The functions are meant to be similar to the React JSX that they will eventually write.
* replace static data with dynamic data pulled from NYT top-stories by topic API.
* generated seed data from NYT top-stories data to populate our own MongoDB database.
* replace NYT data with our own data from MERN back-end.

Here is an example of the functions built to generate the dynamic HTML (very similar to JSX):

```javascript
function getHTMLForArticleSummary(article, topic) {
  
  let imageURL = (article.multimedia)?article.multimedia[0].url:'';

  let articleSummaryHTML = `
    <article>
      <img src="${imageURL}" alt="" />
      <span class="category category-${topic.name}">${topic.title}</span>
      <h3><a href="">${article.title}</a></h3>
      <div class="profile">${article.byline}</div>
      <p>${article.abstract}</p>
    </article>
  `;

  return articleSummaryHTML;
}

async function getHTMLForArticleGrid(topic) {
  let articles = await getArticles(topic.name);
  let articleGridHTML = articles.map(x=>getHTMLForArticleSummary(x, topic)).join("");
  return articleGridHTML;
}

async function showTopic(topic) {
  let element = document.getElementById("showcase");
  element.innerHTML = await getHTMLForShowcaseArticleSummary(topic);
    
  element = document.getElementById("article-grid");
  let articleGridHTML = await getHTMLForArticleGrid(topic);
  element.innerHTML = articleGridHTML;
}

```



#### Header and Showcase Article
![](https://github.com/hoc-labs/images/blob/main/news-site-1.png?raw=true)

#### Article Grid
![](https://github.com/hoc-labs/images/blob/main/news-site-2.png?raw=true)

#### Footer
![](https://github.com/hoc-labs/images/blob/main/news-site-3.png?raw=true)


#### Dynamic Article Content - NYT API
The section and article data is pulled from the NYT API.

![](https://github.com/hoc-labs/images/blob/main/news-site-4.png?raw=true)

#### Dynamic NYT Best Sellers Content - NYT API
The best sellers data is pulled from the NYT API. A dropdown list allows users to change book genre and cause new data to be pulled from the API.

![](https://github.com/hoc-labs/images/blob/main/nyt-books-api.png?raw=true)

#### Dynamic Article Content - MERN back-end
The section and article data is pulled from our MERN back-end.


