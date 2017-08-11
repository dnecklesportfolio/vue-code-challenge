
<template>
  <div id="Dexter">
    <ul>
      <li v-for="user in userStyles">
        {{user.name}}
  
      </li>
    </ul>
    </ul>
    <table>
      <tbody>
        <tr>
          <td colspan="2">
            Name:
            <input v-model.lazy="this.currentUserData[0].name" @keyup.enter="saveNewUser"> </input>
            <button @click.prevent="checkIfUserExists">Load User</button>
            <button @click.prevent="saveNewUser">Save User</button>
  
            <div> {{userExists}}</div>
          </td>
        </tr>
        <tr>
          <td>
            Enter your JSON Style Here
          </td>
          <td>
            Here's what that would look like
          </td>
        </tr>
        <tr v-for="(style,index) in userStyles">
          <td>
            <!-- <input type="text" v-model="style"> -->
            <input type="text" v-model="userStyles[index]" />
          </td>
          <td>
            This is row #{{index}}
          </td>
        </tr>
        <tr>
          <td colspan="2" v-bind:style="{ textAlign: 'left'}">
            <button @click.prevent="addNewStyles">Update</button>
          </td>
        </tr>
  
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'Dexter',
  data() {
    return {
      userExists: '',
      currentUserData: [
        {
          id: 0,
          name: 'Alex',
          styles: ['{"backgroundColor":"yellow"}',
            '{"backgroundColor":"yellow"}'
          ]
        }
      ]
      ,
      allUserData: [
        {
          id: 1, name: 'Dwayne', styles: [
            '{"backgroundColor":"yellow"}',
            '{"backgroundColor":"yellow"}',
          ]
        },
        {
          id: 2, name: 'Alex', styles: [
            '{"backgroundColor":"yellow"}',
            '{"backgroundColor":"yellow"}',
          ]
        },
      ],
      isSubmitted: false,
    }
  },
  computed: {
    userStyles() {
      let currentUser = this.allUserData.filter(element => {
        return element.name == this.currentUserData[0].name;
      })
      return this.currentUserData[0].styles
    },
    userExistedBefore() {
      return this.allUserData.some(element => {
        //console.log("test ",this.currentUserData[0].id )
        if (element.name == this.currentUserData[0].name){
    
          // return element.id == this.currentUserData[0].id     
        }
        return false;
     ;
      })
    }
  },
  methods: {
    addNewStyles() {
      this.userStyles.push('')
    },
    saveNewUser() {

      if (this.userExistedBefore) {       
        this.searchAndUpdate();
        return;

      } else {
        console.log("run here")
        this.allUserData.push({
          id: this.allUserData.length + 1,
          name: this.currentUserData[0].name,
          styles: this.currentUserData[0].styles
        })
      }
      this.currentUserData[0].name = '';
      /* if it does 
       then overwrite name and styles
      */
      /* if it doesnt then
      push in new user
      */
    },
    searchAndUpdate() {
    // https://stackoverflow.com/questions/37585309/replacing-objects-in-array
    // Found concise way but made it verbose for better readablity
    console.log(this.allUserData)
    const step1FindExisting = obj => { 
    return this.currentUserData.find( o => { 
    return o.id === obj.id})
    }

    const step2ReplaceExisting = this.allUserData.map(obj =>{ 
    // If find existing overwrite, else dont change anything
    console.log(step1FindExisting(obj))
    return step1FindExisting(obj) || obj
    });    
    this.allUserData =step2ReplaceExisting
   
    },
    checkIfUserExists() {
      //could this be replaced with a map and find
      for (var i = 0; i < this.allUserData.length; i++) {
        if (this.currentUserName == this.allUserData[i].name) {
          //Set requested user to current user
          this.userExists = "See below";
          this.currentUserData[0].name = this.allUserData[i].name;
          this.currentUserData[0].styles = this.allUserData[i].styles;
          this.currentUserData[0].id = this.allUserData[i].id;
          return;
        } else {
          this.userExists = "This user doesnt exist."
        }
      }
    },
    addNewRow() {
      this.currentArrayOfStyles.push('one')
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
  width: 800px;
  padding: 20px;
}

tr {
  border-bottom: 2px solid gray;
  padding: 20px;
  margin: 0;
}

td {

  border: 2px solid gray;
  padding: 20px;
  text-align: center;
}

input {
  width: 250px;
  padding: 20px;
}
</style>
