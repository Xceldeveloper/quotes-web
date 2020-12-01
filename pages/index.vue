<template>
  <div id="wrapperx">
    <v-toolbar dark absolute width="100%" color="transparent" dense>
      <v-toolbar-title>XcelQuotes</v-toolbar-title>
    </v-toolbar>
    <v-row class="fill-height ma-0" align="center" justify="center">
      <div id="quote-wrapper" >
        <span id="quote-for-day">Quote for the Day</span>
        <blockquote id="quote">
          <span class="q">"</span> {{ quote }} <span class="q">"</span>
        </blockquote>
        <span id="author">~ {{ author }}</span>

        <v-btn id="more-btn" outlined color="#fff" rounded small> More </v-btn>
      </div>
    </v-row>
    <span class="acess">
      Powered by
      <a href="https://zenquotes.io/" target="_blank">ZenQuotes API</a>
    </span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      quote:
        " Make every detail perfect and limit the number of details to perfect",
      author: "Jack Dorsey",
    };
  },
  mounted() {
    this.$axios
      .$get("https://zenquotes.io/api/today")
      .then((data) => {
        this.quote = data[0].q;
        this.author = data[0].a;
        console.log(JSON.stringify(data, 2, null));
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>
<style lang="scss" scoped>
#wrapperx {
  width: 100%;
  height: 100%;
  overflow: auto;
  background: #000;
  position: relative;
}
.fabx {
  position: fixed;
  bottom: 20px;
  right: 20px;
}

.acess {
  font-size: 13px;
  display: block;
  width: 100%;
  text-align: center;
  position: fixed;
  bottom: 0px;
  left: 0px;
  color: #ededed;
  background-color: #000;
}

a {
  text-decoration: none;
}

#quote-wrapper {
  width: 100%;
  max-width: 500px;
  margin: auto;
  text-align: center;
  height: auto;
  padding: 35px;
  display: block;
}

#quote {
  color: #fff;
  font-size: 18px;
}

#author {
  display: block;
  margin: 10px 0px;
  color: #fff;
  font-size: 15px;
}

#quote-for-day {
  display: block;
  margin: 15px 0px;
  width: 100%;
  color: #fff;
  text-align: center;
}

#more-btn {
 
  margin: 35px 0px;
}

.q{
  font-size: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
 
}
</style>
