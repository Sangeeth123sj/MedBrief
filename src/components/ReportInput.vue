<template>
<br/>
<div class="input-report">
    <form @submit.prevent="submitForm">
      
 <div v-if="loadingResult" >
            <strong>Creating a summary..</strong>
          </div>
      <div v-else>
        <br />
      </div>
      <textarea
        class="form-control black-border"
        rows="18"
       
        type="text"
        v-model="text"
        placeholder="input the Report"
        required
      />
      

      <br />
       
      
      <button type="submit" class="submit button-3" role="button">
        Submit <div v-if="loadingResult" >
            <i class="fa fa-spinner fa-spin"></i>
          </div>
      </button>
      
      <button type="button" @click="revertToReport" class="btn btn-outline-success">Back to report</button>
      
    </form>

</div>
</template>
<script>
// import axios from "axios";
import Cookies from "js-cookie";
export default {
  data() {
    return {
      initialPrompt:null,
      loadingResult: false,
      text: "",
      
      
      
    };
  },

  methods: {
    revertToReport(){
      this.text = this.initialPrompt;
    },
    submitForm: function () {
      this.loadingResult = true;
      console.log(this.loadingResult)

      
      // this.text = Cookies.get("report");

     
        try {
          fetch(
            
            // "http://127.0.0.1:8000/summarize/"
            "https://medbriefbackend-production.up.railway.app/summarize/" + this.text,
            // {
            //   headers: {
            //     Accept: "application/json",
            //     Authorization: `Bearer ${this.accessToken}`,
            //   },
            // }
          )
            .then((response) => {
              return response.json();
            })
            .then((data) => {
              console.log(data["summary"]);
              
              this.initialPrompt = this.text;
              this.text = data["summary"];
              this.loadingResult = false;
              // set an HTTP-only cookie with the 'access_token' value
              Cookies.set("report", this.text, { secure: true });
              console.log("cookie report:", Cookies.get("report"))
              console.log("this.text", this.text)
            });
        } catch (error) {
          console.log(error);
          this.text = "Something went wrong please try again";
          this.loadingResult = false;

        }
        
      
      
    },

    
  },

  mounted: function () {},

  computed: {
    
    
    
  },
};
</script>

<style>
/* CSS */
.black-border {
    border: 3px solid black;
}
textarea{
    border:black;
    border:3px;
    top:10%;
}

input[type="range"] {
  filter: lime;
}

.rangers {
  align-items: justify-content;
}
.button-3 {
float: left;
  appearance: none;
  background-color: #2ea44f;
  border: 1px solid rgba(27, 31, 35, 0.15);
  border-radius: 6px;
  box-shadow: rgba(27, 31, 35, 0.1) 0 1px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-family: -apple-system, system-ui, "Segoe UI", Helvetica, Arial,
    sans-serif, "Apple Color Emoji", "Segoe UI Emoji";
  font-size: 14px;
  font-weight: 600;
  line-height: 20px;
  padding: 6px 16px;
  position: relative;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
  white-space: nowrap;
}

.button-3:focus:not(:focus-visible):not(.focus-visible) {
  box-shadow: none;
  outline: none;
}

.button-3:hover {
  background-color: #2c974b;
}

.button-3:focus {
  box-shadow: rgba(46, 164, 79, 0.4) 0 0 0 3px;
  outline: none;
}

.button-3:disabled {
  background-color: #94d3a2;
  border-color: rgba(27, 31, 35, 0.1);
  color: rgba(255, 255, 255, 0.8);
  cursor: default;
}

.button-3:active {
  background-color: #298e46;
  box-shadow: rgba(20, 70, 32, 0.2) 0 1px 0 inset;
}

.image_count {
  font-size: 2px;
}

/* Styling the button */
.advanced-btn {
  cursor: pointer;
  border: 1px solid #3498db;
  background-color: transparent;
  height: 50px;
  width: 200px;
  color: #3498db;
  font-size: 1.5em;
  box-shadow: 0 6px 6px rgba(47, 127, 81, 0.6);
}

.engine-select {
  padding: 20px;
  width: 300px;
}
</style>
