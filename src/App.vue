<template>

  <!--Initial login page From Module 16 Assignment-->
  <div v-if="!isLoggedIn" class="container">
    <h1>Login Box</h1>

    <form @submit.prevent="login">

    <div>
      <label> Password: </label>
      <input type="password" v-model="password" placeholder="enter your password" required>  
    </div>

    <button type="submit">Login</button>
    </form>

    <!--Incorrect password message-->
   <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
  </div>
  

<!--After login successful-->
  <div v-if="isLoggedIn" class="container success">
    <h2> Login Successful</h2>
    <p> You have successfully logged in</p>
    <h2> Book Data</h2>
    <h3>Green = Published</h3>
    <h3>Red = Not Published</h3>
  </div> 

    <!--Call Child boxForm Component-->
    <boxForm  :books=books />
  
</template>



<script>

//Import Child boxForm
import boxForm from './components/boxForm.vue';

//export data
export default {
  name: "App",

  //To Child boxForm
  components: {
    boxForm
  },

  //Define values
  data() {
    return {
       books: [],              //array for data
      password: "cardinals",   //password default
      isLoggedIn: false,
      errorMessage: "",
    };
  },


  //Import from API, check password, login, and pass data to books[]
  methods: {

    //clear password form and API password
     async login() {

      //fetch API
      const res = await fetch("https://cis255.vercel.app/api", {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },

        //Send password to API to gain access to book data
        body: JSON.stringify({ password: this.password })
      });

      //correct Password, entry allowed to API
      if(res.ok) {

            //Login and pass the now available data to books[]
            const data = await res.json();
            console.log(data);
            this.books = data.books;

            this.isLoggedIn= true; 
            this.errorMessage='';
            

      //Incorrect password      
      } else{
          const error = await res.json()
          this.errorMessage = error.message || 'Login failed. Please try again.';
      }
    },
  },
};

</script>

<!--Style Primarily From Module 16 Assignment-->
<style>
/* Import Google Font */
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
/* Set body font */
body {
  font-family: 'Montserrat', sans-serif;
  background-color:rgb(253, 248, 241);
}

/* Container for login form and success message */
.container {
  max-width: 400px;           /* Maximum width */
  margin: 30px auto;          /* Center horizontally with top margin */
  overflow: auto;             /* Handle overflow content */
  min-height: 300px;          /* Minimum height */
  border: 0.3em solid black;  /* Black border */
  padding: 30px;              /* Internal spacing */
  border-radius: 15px;         /* Rounded corners */
}

/* Spacing for divs */
div {
  margin-bottom: 0.5em;
}

/* Style for input fields */
input {
  width: 100%;                /* Full width */
  padding: 10px;              /* Internal spacing */
  margin: 10px 0;             /* Top and bottom margin */
  border: 1px solid #ddd;     /* Light gray border */
  border-radius: 4px;         /* Slightly rounded corners */
}

/* Style for buttons */
button {
  width: 100%;                /* Full width */
  padding: 10px;              /* Internal spacing */
  background-color: #8741f7;  /* Pur background */
  color: white;               /* White text */
  border: none;               /* No border */
  border-radius: 10px;         /* Slightly rounded corners */
  cursor: pointer;            /* Show pointer cursor on hover */
  font-size: 16px;            /* Font size */
}

/* Button hover effect */
button:hover {
  background-color: #7a27ff;  /* Darker Pur on hover */
}

/* Error message styling */
.error {
  color: rgb(214, 0, 0);                 /* Red text for errors */
  margin-top: 10px;           /* Space above error message */
}

/* Success message styling */
.success {
  background-color: #f2e9ff;  /* Light green background */
  border-color: #7a27ff;      /* Pur border */
  color: #4c00c7;             /* Dark Pur text */
  text-align: center;         /* Center text */
}
.success h2 {
  color: #4c00c7;             /* Pur color for checkmark and heading */
  margin-bottom: 15px;        /* Space below heading */
}
</style>
