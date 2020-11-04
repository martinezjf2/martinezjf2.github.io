---
layout: post
title:      "How to create a Search "
date:       2020-11-04 19:15:20 +0000
permalink:  how_to_create_a_search
---


A [link](https://github.com/martinezjf2/react) to my project would be provided to follow along

There are many ways to create a search bar with there being a easier way by making an input field on the component where you are rendering you data, or you can make it a little more complex as a separate component. [CLICK HERE](https://github.com/martinezjf2/react) to clone my repo and follow along what I have implemented.

## Let’s Get Started!

First of all, i had to decide where I would have to implement my filter method and my events. I created my function within my UniversityContainer. The reason on doing this was because i have my `mapStateToProps` which gives me my data (in this case state.universities) which was pulled out from my store in Redux with {connect}.  



`class UniversityContainer extends Component {

    constructor(){
		
        super();
				
        this.state = {
				
            universitiesArray: [],
						
            searchfield: ''
						
        }
				
    }`

ES6 class constructors MUST call super if they are subclasses. For more information [click here](https://www.digitalocean.com/community/tutorials/react-constructors-with-react-components) 

 I created a state for universitiesArray as an empty array and a searchfield as an empty string.

### Creating my onSearchChange function


`
onSearchChange = (e) => {

        this.setState({
				
            universitiesArray: this.props.universities,
						
            searchfield: e.target.value 
						
        })
				
    }`

Within this function i used [setState](https://reactjs.org/docs/state-and-lifecycle.html/) to make changes to the component state 

I set my universitiesArray to be the universities within my props and the searchfield would be set up as the value of what I am inputting within my field.


#### We are almost there!

### Iteration


`render() {


        const filteredUniversities = this.props.universities.filter((university) => {
				
            return university.name.toLowerCase().includes(this.state.searchfield.toLowerCase());			
						
        })
				
        return (…)}`
				

Within my render, I made a variable set to my universities then used the [filter method](https://levelup.gitconnected.com/using-the-filter-function-in-javascript-and-react-317ff155da73)
Which will take in a callback function and it will create a new array, and then filter the contents of the original array, based on the callback’s parameters, into the new array.



I made sure that when i type in a lowercase a i also want the the universities that would have a capitalized A as well so in the case i implemented university.name.toLowercase() and the includes would give me all the universities that contain that letter. I set the state.searchfield as its argument, and also made sure to lowercase.

### So now what is next?

Well, in order for me to create my class component and make my searchbar function i have to pass down my onSearchChange as a prop and pass in my filteredUniversities as well within my return. For Example:

`return (

            <div>
						
                <Switch>
								
                <Route exact path="/universities"  render={(routerProps) => <Universities {...routerProps} universities=
								{filteredUniversities} onSearchChange={this.onSearchChange}/>} />        
								
               </Switch>
							 
            </div>
						
        )`



### Creating a SearchBar Class Component

For a searchbar, we should not have to make it a class component, it is most recommended to use a functional component because it is not going to have any state. But for this exercise we will do it as a class component. 


`import React from 'react'

class Searchbar extends React.Component{

    constructor(props) {
		
        super(props)
				
    }
		
    render() {
		
        return (
				
            <div>
						
                <label>Search: </label>
								
                <input type="text"  
								
                name="search"
							
								
                onChange={this.props.onSearchChange}
								
                /> <br/> <br/>
               
            </div>
						
        )
				
    	}
			
    }
		
export default Searchbar`


So we want to make sure that when making a class component we pass down props within the constructor that we will be passing soon within our Universities Functional Component. The most important thing within our input field is having our onChange set to the onSearchChange prop that was passed down. 

Last Step: Universities Functional Component

This is where i want to display my search bar. In order for me to use this component i have to import it on top as an import statement.


import Searchbar from './Searchbar'

Next I have to make that component visible on my UI by implementing it within my return and make sure i pass down the onSearchChange as a prop so i can use within the SearchBar Class Component.





`return (

        <div>
				
            <h1 className="schoolSearch">School Search</h1>
						

            <Searchbar onSearchChange={props.onSearchChange}/>

…

)`



Testing it out! It is important to test your code. I really do help this helps. Thank You!





