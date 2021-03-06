So let's define the graphql subscription to be used.

Open `src/Todo/TodoQueries.js` and add the following code:

```

const SUBSCRIPTION_ONLINE_USERS = gql`
  subscription {
    online_users(order_by: name_asc) {
      name
    }
  }
`;

export {
  SUBSCRIPTION_ONLINE_USERS
};

```


Open `src/Todo/OnlineUsers.js` and add the following imports:

```
import { Subscription } from "react-apollo";
import { SUBSCRIPTION_ONLINE_USERS } from "./TodoQueries";
```

We are importing the `Subscription` component from `react-apollo` and the graphql subscription query we defined above to fetch the online user data.

Now, we will wrap the component with `Subscription` passing our graphql mutation constant that we imported. Replace the `return` with the following code:

```
      <Subscription subscription={SUBSCRIPTION_ONLINE_USERS}>
        {({ loading, error, data }) => {
          if (loading) {
            return <div>Loading. Please wait...</div>;
          }
          if (error) {
            return <div>Error loading users</div>;
          }
          return (
            ...your original return react code
          );
        }}
      </Subscription>
```

Now that we have the real data, let's remove the mock online user data constant.

How does this work?
-------------------
We are using the `<Subscription>` component which gives render props (similar to `<Query>` and `<Mutation>` components). The `data` prop gives the result of the realtime data for the query we have made.

Refresh your react app and see yourself online! There could be other users online as well.

Awesome! You have completed basic implementations of a GraphQL Query, Mutation and Subscriptions. Easy isn't it?

