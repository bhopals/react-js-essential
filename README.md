


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




### Props and STATE ###

**Compose Components** - This means we have multiple nested components. Parent Component that contains multiple/single child components, and the data in these components have been passed from the top hierarchy 
to bottom. 

```
const Book = ({title, author, pages}) => {
	return (
		<section>
			<h2>{title}</h2>
			<p>by: {author}</p>
			<p>Pages: {pages} pages</p>
		</section>
	)
}

const Library = () => {
	return (
		<div>
			<Book title="The Sun Also Rises" author="Ernest Hemingway" pages={260}/>
			<Book title="White Teeth" author="Zadie Smith" pages={480}/>
			<Book title="Cat's Cradle" author="Kurt Vonnegut" pages={304}/>
		</div>
	)
}

render(
	<Library />, 
	document.getElementById('root')
)
```


**Iteration over the Child Components**

```
        let bookList = [
            {"title": "Hunger", "author": "Roxane Gay", "pages": 320},
            {"title": "The Sun Also Rises", "author": "Ernest Hemingway", "pages": 260},
            {"title": "White Teeth", "author": "Zadie Smith", "pages": 480},
            {"title": "Cat's Cradle", "author": "Kurt Vonnegut", "pages": 304}
        ]

        const Book = ({title, author, pages}) => {
            return (
                <section>
                    <h2>{title}</h2>
                    <p>by: {author}</p>
                    <p>Pages: {pages} pages</p>
                </section>
            )
        }

        const Library = ({books}) => {
            return (
                <div>
                    {books.map(
                        (book, i) => 
                            <Book 
                                key={i}
                                title={book.title} 
                                author={book.author} 
                                pages={book.pages}/>
                    )}
                </div>
            )
        }



        render(
            <Library books={bookList}/>, 
            document.getElementById('root')
        )


```



**State**

```
        let bookList = [
            {"title": "Hunger", "author": "Roxane Gay", "pages": 320},
            {"title": "The Sun Also Rises", "author": "Ernest Hemingway", "pages": 260},
            {"title": "White Teeth", "author": "Zadie Smith", "pages": 480},
            {"title": "Cat's Cradle", "author": "Kurt Vonnegut", "pages": 304}
        ]

        const Book = ({title, author, pages}) => {
            return (
                <section>
                    <h2>{title}</h2>
                    <p>by: {author}</p>
                    <p>Pages: {pages} pages</p>
                </section>
            )
        }

        class Library extends React.Component {
            
            state = { open: false }

            toggleOpenClosed = () => {
                //Using Callback
                this.setState(prevState => ({
                    open: !prevState.open
                }))

                //Using Properties
                this.setState({
                    open: !this.state.open
                })
            }
            render() {
                const { books } = this.props
                return (
                    <div>
                        <h1>The library is {this.state.open ? 'open' : 'closed'}</h1>
                        <button onClick={this.toggleOpenClosed}>Change</button>
                        {books.map(
                            (book, i) => 
                                <Book 
                                    key={i}
                                    title={book.title} 
                                    author={book.author} 
                                    pages={book.pages}/>
                        )}
                    </div>
                )
            }
        }



        render(
            <Library books={bookList}/>, 
            document.getElementById('root')
        )
```

The constructor in Class is used to bind Methods, initialize state and super class constructor.

```
    class Library extends React.Component {

        constructor(props){
            super(props);
            this.state = {
                open:false
            }
            //Method Binding
            this.toggleOpenClosed = this.toggleOpenClosed.bind(this);

        }  
        state = { open: false }

        toggleOpenClosed () {
            //Using Callback
            this.setState(prevState => ({
                open: !prevState.open
            }))
    }
```

Alternate of the above syntax is:

```
        class Library extends React.Component {
                
            state = { open: false }
            
            //With the use of arrow function, binding of "this is happening automatically"
            toggleOpenClosed = () => {
                //Using Callback
                this.setState(prevState => ({
                    open: !prevState.open
                }))
        }
```



**Component Life Cycle**

- constructor: to initialize state

- render: Method is called when there is any change 

- componentDidMount: Only once when the component is Mounted the very first time. 
    Right after the component added to the DOM. To Load data from any WEB Service.

- componentDidUpdate: Whenever any state / props changed, this life cycle method will be called.

- componentWillUnmount: This will be called before the unmounting of the components. Mainly used to release Network resource, garabase collection, Object memory release. In short, do any short of clean up.


```

    componentDidMount() {
		console.log("The component is now mounted!")
	}

	componentDidUpdate() {
		console.log("The component just updated")
	}


    componentWillUnmount() {
		console.log("The component just updated")
	}

```


**Loading Data from the API**

```
    componentDidMount() {
		this.setState({loading: true})
		fetch('https://hplussport.com/api/products/order/price/sort/asc/qty/1')
			.then(data => data.json())
			.then(data => this.setState({data, loading: false}))
	}



     <div>
            {this.state.hiring ? <Hiring /> : <NotHiring />}
            {this.state.loading 
                ? "loading..."
                : <div>
                    {this.state.data.map(product => {
                        return (
                            <div>
                                <h3>Library Product of the Week!</h3>
                                <h4>{product.name}</h4>
                                <img src={product.image} height={100}/>
                            </div>
                        )
                    })}
                    
                </div>
            }
        </div>
```

**Submit Form Data**

```
    class FavoriteColorForm extends React.Component {
        state = { value: ''}

        newColor = e => 
            this.setState({ value: e.target.value })

        submit = e => {
            console.log(`New Color: ${this.state.value}`)
            e.preventDefault()
        }

        render() {
            return (
                <form onSubmit={this.submit}>
                    <label>
                        Favorite Color: 
                        <input 
                            type="color"
                            onChange={this.newColor} />
                    </label>
                    <button>Submit</button>
                </form>
            )
        }
    }

```


**DefaultProps**
The defaults values to be used in case the state or prop objet in null or empty.
This is used to supply default values when other values are not provided. Basically, to save the app
from breaking in case of data is not available.

```
Class Syntax - Use the static property provided
    class Library extends React.Component {

        static defaultProps = {
            books: [
                {"title": "Tahoe Tales", "author": "Chet Whitley", "pages": 1000}
            ]
        }

        

Function Syntax - Use default arguement syntax :

const Book = ({title="No Title Provided", author= "No Author", pages=0, freeBookmark}) => {
	return (
		<section>
			<h2>{title}</h2>
			<p>by: {author}</p>
			<p>Pages: {pages} pages</p>
			<p>Free Bookmark Today: {freeBookmark ? 'yes!': 'no!'}</p>
		</section>
	)
}


```

**PropTypes**
Sometimes we expect sepecfic Property Types to be passed in our component. Using propTypes, we can 
ensure that correct type of data is passed to the component. To use this 

1. First we need to import "PropType" 
    import PropTypes from "prop-types"

2. Npm install
    npm install prop-types

3. Add the prop types condition for any component

    Library.propTypes = {
        books : PropTypes.array,
    }

    Book.propTypes = {
        title : PropTypes.string,
        author : PropTypes.string,
        pages : PropTypes.number,
        freeBookmark : PropTypes.bool
    }

4. You are done. :)




**Build your Project**
To deploy you can use Heroku, Netlify, Zite or some other hosting provider

 - First we need to make the production ready build. We can do that using command "npm run build"
 
 - Once build is completed, it can be tested using static server. For that we need to install npm serve
  " npm install serve -g"

- To serve the build, we need to run "serve -s build" 

- Thats it.

To have the more Advance React tutorial, you can explore

    -   React Recipes
    -   React : Lifecycles
    -   React : Components, Context, and Accessibility




- To practice online React App you can use **https://codesandbox.io/s/new**

- For quick intro on REACT, there is article that explains all the features and there overview in REACT.

  A React [Handbook](https://medium.freecodecamp.org/the-react-handbook-b71c27b0a795)



More Handbooks, kindly refer below link:
https://flaviocopes.com/page/ebooks/