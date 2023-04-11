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

- Course outcomes
  - props types
    - built-in data type props
    - user defined data type props
    - events props
  - hooks types

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

// void
const handleClick = (): void => {
  console.log("clicked");
};
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

  // one more array example

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";
  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User users={users} />
      </div>
    );
  }
  export default App;

  // User.tsx
  import React from "react";
  type UserProps = {
    users: {
      id: number;
      name: string;
      email: string;
    }[];
  };
  const User = ({ users }: UserProps) => {
    return (
      <div>
        {users.map((user) => {
          const { id, name, email } = user;
          return (
            <div key={id} style={{ border: "1px solid", margin: "1rem" }}>
              <p>{name}</p>
              <p>{email}</p>
            </div>
          );
        })}
      </div>
    );
  };
  export default User;
  ```

- union of types

  ```tsx
  // Message.tsx
  import React from "react";

  type MessageProps = {
    text: "ADD" | "UPDATE" | "DELETE";
  };

  const Message = (props: MessageProps) => {
    if (props.text === "ADD") {
      return <p>User is added</p>;
    } else if (props.text === "UPDATE") {
      return <p>User is updated</p>;
    }
    return <p>User is deleted</p>;
  };

  export default Message;

  // App.tsx
  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <Message text="UPDATE" />
        {/* <User users={users} /> */}
      </div>
    );
  }

  export default App;
  ```

- children props

  ```tsx
  // Card.tsx
  import React from "react";
  type CardProps = {
    children: React.ReactNode;
  };
  const Card = (props: CardProps) => {
    return <div className="card">{props.children}</div>;
  };

  export default Card;

  //User.tsx
  import React from "react";
  import Card from "./Card";

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
      <Card>
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
      </Card>
    );
  };
  export default User;
  ```

## 5. Typing Event Props

- example

  ```tsx
      // Typing event props
    click event: event: React.MouseEvent<HTMLButtonElement>
    type ButtonProps = {
    handleClick: (event: React.MouseEvent<HTMLButtonElement>) => void;
    handleChange: (event: React.ChangeEvent<HTMLInputElement>) => void
    };

    //App.tsx
    import React, { useState } from "react";

    type NewUserProps = {
      name: string;
      email: string;
    };
    const NewUser = () => {
      const [user, setUser] = useState<NewUserProps>({ name: "", email: "" });

      const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
        const fieldName = event.target.name;
        setUser({ ...user, [fieldName]: event.target.value });
      };

      const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
        event.preventDefault();
        console.log(user);
      };


      const handleSubmit = (event: FormEvent<HTMLFormElement>) => {
        event.preventDefault();
        const newTodo = { id: Math.random().toString(), title };
        onAddNewTodo(newTodo);

          // const target = event.target as typeof event.target & {
          //   title: { value: string };
          // };
          // console.log(target.title.value);
      };
      return (
        <div>
          <h2>Create User</h2>
          <form onSubmit={handleSubmit}>
            <div>
              <label htmlFor="name">
                Name
                <input
                  type="text"
                  id="name"
                  name="name"
                  value={user.name}
                  onChange={handleChange}
                  required
                />
              </label>
            </div>
            <div>
              <label htmlFor="email">
                Email
                <input
                  type="email"
                  id="email"
                  name="email"
                  value={user.email}
                  onChange={handleChange}
                  required
                />
              </label>
            </div>
            <button type="submit">Create User</button>
          </form>
        </div>
        );
      };

      export default NewUser;

  ```

## 6. Style Props

- example

  ```tsx
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
  ```

## 7. Typing useState Hooks

- example

  ```tsx
  import React, { useState } from "react";
  import "./App.css";

  const App = () => {
    // type is automatically infereed as number
    const [count, setCount] = useState(0);

    const handleIncrement = (): void => {
      setCount((count) => count + 1);
    };

    const handleDecrement = (): void => {
      setCount((count) => count - 1);
    };

    return (
      <div className="App">
        <h1>Count : {count}</h1>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
      </div>
    );
  };

  export default App;

  // dealing with future values in useState Hook
  import React, { useState } from "react";
  import "./App.css";

  type User = {
    id: number;
    name: string;
  };

  const App = () => {
    // const [data, setData] = useState<null | string>(null);
    const [data, setData] = useState<null | User>(null);

    const handleSetData = () => {
      // setData("Anisul islam");
      setData({ id: 101, name: "anisul islam" });
      console.log(data);
    };

    return (
      <div className="App">
        <h1>UseState Future value</h1>
        <button onClick={handleSetData}>set data</button>
        {/* {data && <p>{data}</p>} */}
      <!-- <p>{data?.id}</p> -->
      <!-- <p>{data?.name}</p> -->
      </div>
    );
  };

  export default App;

  // type asertion - without optional chaining operator
  import React, { useState } from "react";
  import "./App.css";

  type User = {
    id: number;
    name: string;
  };

  const App = () => {
    // const [data, setData] = useState<null | string>(null);
    const [data, setData] = useState<User>({} as User);

    const handleSetData = () => {
      // setData("Anisul islam");
      setData({ id: 101, name: "anisul islam" });
      console.log(data);
    };

    return (
      <div className="App">
        <h1>UseState Future value</h1>
        <button onClick={handleSetData}>set data</button>
        {/* {data && <p>{data}</p>} */}
        <p>{data.id}</p>
        <p>{data.name}</p>
      </div>
    );
  };

  export default App;
  ```

## 8. Typing useReducer Hooks

- example

  ```tsx
  // Counter.tsx
  import React, { useReducer } from "react";

  const INCREMENT = "INCREMENT";
  const INCREMENTBYAMOUNT = "INCREMENTBYAMOUNT";
  const RESET = "RESET";
  const DECREMENT = "DECREMENT";

  const initialState = { count: 0 };
  type counterState = {
    count: number;
  };

  type IncrementActionType = { type: typeof INCREMENT };
  type IncrementByAmountActionType = {
    type: typeof INCREMENTBYAMOUNT;
    payload: number;
  };
  type ResetActionType = { type: typeof RESET };
  type DecrementActionType = { type: typeof DECREMENT };

  type counterActionType =
    | IncrementActionType
    | DecrementActionType
    | ResetActionType
    | IncrementByAmountActionType;

  const reducer = (state: counterState, action: counterActionType) => {
    switch (action.type) {
      case INCREMENT:
        return { count: state.count + 1 };
      case INCREMENTBYAMOUNT:
        return { count: state.count + action.payload };
      case RESET:
        return { count: 0 };
      case DECREMENT:
        return { count: state.count - 1 };
      default:
        throw new Error();
    }
  };

  const Counter = () => {
    const [state, dispatch] = useReducer(reducer, initialState);
    return (
      <div>
        <h1> Count : {state.count}</h1>
        <button
          onClick={() => {
            dispatch({ type: INCREMENT });
          }}
        >
          Increment
        </button>
        <button
          onClick={() => {
            dispatch({ type: INCREMENTBYAMOUNT, payload: 5 });
          }}
        >
          IncrementByAmount
        </button>
        <button
          onClick={() => {
            dispatch({ type: RESET });
          }}
        >
          Reset
        </button>
        <button
          onClick={() => {
            dispatch({ type: DECREMENT });
          }}
        >
          Decrement
        </button>
      </div>
    );
  };

  export default Counter;
  ```
