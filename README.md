## basic props type

- why ts?
  - auto suggestion / auto completion
  - easy debugging
  - better documentation
- example of basic props type

  ```js
    // component props is an object
    <!-- let name: string
    let age: number  -->

    type UserProps = {
        name: string;
        age: number;
      };

     // const User = (props: UserProps) => {

    // const User = (props: { name: string, age: number }) => {
    const User = ({name, age}: { name: string, age: number }) => {
      return (
      <div>
        <h2>
          {props.name} is {props.age} years old
        </h2>
      </div>
    );
  };

  export default User;

  import "./App.css";
  import User from "./components/User";

  function App() {
    return (
      <div className="App">
        <User name="Anisul" age={32} />
      </div>
    );
  }

  export default App;


  // more
    import "./App.css";
  import User from "./components/User";


      let location = {
      city: "Tampere",
      country: "Finland",
      };

      let languages = ["Bangla", "English", "Finnish"];

      function App() {
        return (
        <div className="App">
          <User
                  name="Rabeya"
                  age={31}
                  isLoggedIn={true}
                  location={location}
                  languages={languages}
                />
        </div>
        );
      }

      export default App;


      import React from "react";

      type UserProps = {
        name: string;
        age: number;
        isLoggedIn: boolean;
        location: {
          city: string;
          country: string;
        };
        languages: string[];
      };

      const User = (props: UserProps) => {
        return (
          <div>
            {props.isLoggedIn && (
              <div>
                <h2>
                  {props.name} is {props.age} years old.
                </h2>
                <p>
                  Address: {props.location.city}, {props.location.country}
                </p>
                <p>
                  Speaks:
                  {props.languages.map((language, index) => {
                    return <span key={index}> {language} </span>;
                  })}
                </p>
              </div>
            )}
          </div>
        );
      };

      export default User;


    // children passing
    import React from "react";

    type HeadingProps = {
      children: string;
    };

    const Heading = (props: HeadingProps) => {
      return <p>{props.children}</p>;
    };

    export default Heading;

      <Heading>Anisul Islam</Heading>


      // component type: React.ReactNode
      // passing components inside components
      import React from "react";

      type HeadingProps = {
        children: React.ReactNode;
      };

      const Heading = (props: HeadingProps) => {
        return <div>{props.children}</div>;
      };

      export default Heading;

        <Heading>
        <Text />
      </Heading>


      // Typing event props
      click event: event: React.MouseEvent<HTMLButtonElement>
      type ButtonProps = {
        handleClick: (event: React.MouseEvent<HTMLButtonElement>) => void;
          handleChange: (event: React.ChangeEvent<HTMLInputElement>) => void
      };

      // props for styles -> React.CSSProperties
        import React from "react";

          type ButtonProps = {
            styles: React.CSSProperties;
          };

          const Button = (props: ButtonProps) => {
            return <button style={props.styles}>click me</button>;
          };

          export default Button;

          import "./App.css";
          import Button from "./components/Button";

          function App() {
            return (
              <div className="App">
                <Button
                  styles={{ backgroundColor: "green", padding: "1rem", color: "white" }}
                />
              </div>
            );
          }

          export default App;

        // tips
        // 1. destructure props
        // 2. create file name as Person.types.ts and export the types so that you can import from anywhere
  ```
