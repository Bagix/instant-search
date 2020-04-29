<template>
  <div class='container'>
    <label for="search">Search by title</label>
    <input id="search" class="search-input" type="text" v-model="searchText">
    <ul class="list">
      <li class="list__item"
      target="_blank"
      v-for='article in filteredArticles'
      :key='article.title'>
        <a :href="article.url">
          <img :src="article.image">
          <h3>{{ article.title }}</h3>
        </a>
      </li>
    </ul>
    <transition name="slideIn">
      <h3 class="msg-empty" v-if="empty">No matching results for: <span>{{ searchText }}</span></h3>
    </transition>
  </div>
</template>zdsc

<script>
export default {
  name: 'InstantSearch',
  data() {
    return {
      searchText: '',
      empty: false,
      articles: [
        {
          title: 'What You Need To Know About CSS Variables',
          url: 'https://tutorialzine.com/2016/03/what-you-need-to-know-about-css-variables/',
          image: 'https://tutorialzine.com/media/2016/03/css-variables.jpg'
        },
        {
          title: 'Freebie: 4 Great Looking Pricing Tables',
          url: 'https://tutorialzine.com/2016/02/freebie-4-great-looking-pricing-tables/',
          image: 'https://tutorialzine.com/media/2016/02/great-looking-pricing-tables.jpg'
        },
        {
          title: '20 Interesting JavaScript and CSS Libraries for February 2016',
          url: 'https://tutorialzine.com/2016/02/20-interesting-javascript-and-css-libraries-for-february-2016/',
          image: 'https://tutorialzine.com/media/2016/02/interesting-resources-february.jpg'
        },
        {
          title: 'Quick Tip: The Easiest Way To Make Responsive Headers',
          url: 'https://tutorialzine.com/2016/02/quick-tip-easiest-way-to-make-responsive-headers/',
          image: 'https://tutorialzine.com/media/2016/02/quick-tip-responsive-headers.png'
        },
        {
          title: 'Learn SQL In 20 Minutes',
          url: 'https://tutorialzine.com/2016/01/learn-sql-in-20-minutes/',
          image: 'https://tutorialzine.com/media/2016/01/learn-sql-20-minutes.png'
        },
        {
          title: 'Creating Your First Desktop App With HTML, JS and Electron',
          url: 'https://tutorialzine.com/2015/12/creating-your-first-desktop-app-with-html-js-and-electron/',
          image: 'https://tutorialzine.com/media/2015/12/creating-your-first-desktop-app-with-electron.png'
        }
      ]
    }
  },
  computed: {
    filteredArticles: function() {
      let articlesArray = this.articles
      const phrase = this.searchText

      if(this.text === '') return articlesArray

      articlesArray = articlesArray.filter(el => el.title.toLowerCase().indexOf(phrase) !== -1)
      return articlesArray
    }
  },
  watch: {
    filteredArticles: function(val) {
      if(val.length === 0) {
        this.empty = true
      } else {
        this.empty = false
      }
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style lang='scss'>
* {
  box-sizing: border-box;
}
:root {
  --dark: #161D20;
  --blue: #36498F;
  --light-blue: #2D7C9D;
  --gray: #A4A29E;
  --light-gray: #CCC;
}

body {
  background-color: var(--dark);
  color: var(--light-gray);
}

.container {
  width: 100%;
  max-width: 1200px;
  margin: auto;
  padding: 1rem;
}

.search-input {
  font-size: 1.1rem;
  background-color: transparent;
  border-top: none;
  border-right: none;
  border-left: none;
  border-bottom: 1px solid var(--gray);
  color: var(--light-gray);
  padding: .33rem .75rem;
  &:focus {
    outline: none;
  }
}

.list {
  margin:L 0;
  padding: 0;
  list-style: none;
  background-color: var(--blue);
  border-radius: 3px;
  &__item {
    &:first-of-type {
      a {
        border-top-left-radius: 3px;
        border-top-right-radius: 3px;
      }
    }
    &:last-of-type {
      a {
        border-bottom-left-radius: 3px;
        border-bottom-right-radius: 3px;
      }
    }
    & > a {
      display: block;
      padding: 1rem 0;
      color: var(--light-gray);
      text-decoration: none;
      background-color: transparent;
      transition: background-color .25s linear;
      img {
        width: 200px;
        height: auto;
      }
      &:hover {
        background-color: var(--light-blue);
      }
    }
  }
}

.msg-empty {
  color: var(--gray);
  span {
    text-decoration: underline;
  }
}

.slideIn {
  &-enter {
    margin-top: 50px;
    opacity: 0;
  }
  &-enter-active {
    transition: all .5s linear;
  }
}

</style>
