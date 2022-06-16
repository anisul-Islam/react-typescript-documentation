# React + Typescript documentation

- prerequisities - TypeScript, React Fundamentals

## 1. Introduction to TypeScript

- What is TypeScript?

  - programming language developed by microsoft
  - superset of JavaScript

- Why TypeScript?

  - adds static typing to JavaScript
  - it helps to see bugs when writing codes; easy to find and fix bugs
  - gives auto suggestion
  - provides better documentation

## 2. Environment setup

- install node & VSCode
- install react+ts -> `npx create-react-app appName --template typescript`

## 3. typescript for Props - built in types

- built in types example -> string, number, boolean
- extension .ts and component extension is .tsx not .js or .jsx

```tsx
// auto completion -> props.
// if we pass anything other than string as name props we will get error
// component props is an object
// User.tsx (version-1)
import React from "react";
const User = (props: {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
}) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{props.name}</h2>
      <p>{props.email}</p>
      <p>{props.age} years old</p>
      {props.isRegistered ? (
        <p>Registered Student</p>
      ) : (
        <p>Unregistered Student</p>
      )}
    </div>
  );
};

export default User;

// User.tsx (version-2)
import React from "react";

type UserProps = {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
};
const User = (props: UserProps) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{props.name}</h2>
      <p>{props.email}</p>
      <p>{props.age} years old</p>
      {props.isRegistered ? (
        <p>Registered Student</p>
      ) : (
        <p>Unregistered Student</p>
      )}
    </div>
  );
};
export default User;

// User.tsx (version-3)
import React from "react";
type UserProps = {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
};
const User = ({ name, email, age, isRegistered }: UserProps) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{name}</h2>
      <p>{email}</p>
      <p>{age} years old</p>
      {isRegistered ? <p>Registered Student</p> : <p>Unregistered Student</p>}
    </div>
  );
};
export default User;

// App.tsx
import React from "react";
import "./App.css";
import User from "./components/User";

function App() {
  return (
    <div className="App">
      <h1>User Management App</h1>
      <User
        name="anisul islam"
        email="anisul2010s@yahoo.co.uk"
        age={32}
        isRegistered={true}
      />
      <User
        name="Rabeya Begum"
        email="rabu2010s@yahoo.co.uk"
        age={31}
        isRegistered={false}
      />
    </div>
  );
}

export default App;
```

## 4. typescript for Props - User defined types

- Object, Array, Union, enum, tuple, any, custom type

- object props

  ```tsx
  import React from "react";

  type UserProps = {
    user: {
      name: string;
      email: string;
      age: number;
      isRegistered: boolean;
    };
  };
  const User = ({ user }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
        <p>{user.age} years old</p>
        {user.isRegistered ? (
          <p>Registered Student</p>
        ) : (
          <p>Unregistered Student</p>
        )}
      </div>
    );
  };

  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const user1 = {
    name: "anisul islam",
    email: "anisul2010s@yahoo.co.uk",
    age: 32,
    isRegistered: true,
  };
  const user2 = {
    name: "Rabeya Begum",
    email: "rabu2010s@yahoo.co.uk",
    age: 31,
    isRegistered: false,
  };

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User user={user1} />
        <User user={user2} />
      </div>
    );
  }

  export default App;

  // more updates for App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
      age: 32,
      isRegistered: true,
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
      age: 31,
      isRegistered: false,
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        {users.map((user) => (
          <User key={user.id} user={user} />
        ))}
      </div>
    );
  }

  export default App;
  ```

- array props

  ```tsx
  // simple example
  import React from "react";

  type UserProps = {
    lang: string[];
  };
  const User = ({ lang }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <p>
          Speaks:{" "}
          {lang.map((language, index) => {
            return <span key={index}>{language} </span>;
          })}
        </p>
      </div>
    );
  };
  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";
  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User lang={["Bangla", "English", "Finnish"]} />
      </div>
    );
  }
  export default App;

  // complex example
  import React from "react";

  type UserProps = {
    user: {
      name: string;
      email: string;
      age: number;
      isRegistered: boolean;
      languages: string[];
    };
  };
  const User = ({ user }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
        <p>{user.age} years old</p>
        {user.isRegistered ? (
          <p>Registered Student</p>
        ) : (
          <p>Unregistered Student</p>
        )}
        <p>
          Speaks:{" "}
          {user.languages.map((language, index) => {
            return <span key={index}>{language} </span>;
          })}
        </p>
      </div>
    );
  };
  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
      age: 32,
      isRegistered: true,
      languages: ["Bangla", "English"],
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
      age: 31,
      isRegistered: false,
      languages: ["Bangla", "English", "Finnish"],
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        {users.map((user) => (
          <User key={user.id} user={user} />
        ))}
      </div>
    );
  }
  export default App;
  ```

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

```

```

```
