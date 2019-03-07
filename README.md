


## REACT JS Essential ##


#### React is a JavaScript Library that is used to build User Interfaces. With React we can create reusable components, and these component displays data as it changes over time. ### 

The Prime reason that react is very popular is because of its Component Based Structure.
It helps us to create nested collection of component to render the screen or user interface.



### React Start ###

**Install Create React app**
 ```
 npm install -g create-react-app
 ```


**React APP Generator** - https://reactjs.org/docs/create-a-new-react-app.html

Navigate to the directory you want to generate your app 

```
create-react-app <project_name>
``` 

Once the project is generated, you will see "package.json" file, and in that file there would be some 
dependecy installed .

    -   react : Main React Library which allows us to create React Component and use the React Library 
    -   react-dom : React Dom is to take those component and place them in the dom to render them on page.
    -   react-script : transpiling of new syntax, also the WEBPack and other behind the scene things 

    
### React Elements ###
There are two ways to create REACT Element. 

1. Using React.createElement Method

```
        const title = React.createElement(
            'h1',
            {},
            'Welcome!!'
        );

        ReactDOM.render(
            title,
            document.getElementById('root');
        )

```


2.  Using JSX(Javascript as XML) - TAG Based Syntax

```
        ReactDOM.render(
            <div>
                <h1>Welcome</h1>
                <p>Happy to assist!!</p>
            </div>,

            document.getElementById('root');

        )

```


### React Component ###


1. Create React Component using ES6 Class Syntax.

```
class Message extends React.Component {
   
    getMyName = function() {
     return "Hi There!!!"
    }

    render() {

        return (
            <div> 
                Hello {this.props.name}
                Function {this.getMyName}
            </div>
        )
    }
}

ReactDOM.render(<Message name="BHOPAL" />,document.getElementById('root'));

```

2. Create a component as a Function.

```
const getMyName = function() {
    return "Hi There!!!"
}
const Message = (props) => {

    return (
            <div> 
                Hello {props.name}
                Function {getMyName}
            </div>
        )
}

ReactDOM.render(<Message />,document.getElementById('root'));


```






**JSX allow us to access dynamic data by using "this.props" object.

Note : 
    -   All the REACT Components have "render()" method which describes what would be the body of the component.
    -   React Component name should be Capitalize/UpperCase letter to distinguish between regular JSX element and React Element.
    - If we use Class Component then we this.props would contain all the properties passed from the component.
    - In case of Function compoment, we do not have the access of "this", hence we need to pass the "props" reference or can use "desctructing"
    example :
    //properties - props.name, props.age
    const Message = (props) => {
        
    const Message = ({name, age}) => {
