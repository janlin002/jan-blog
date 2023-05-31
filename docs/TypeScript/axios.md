# axios

[Making HTTP requests with Axios in TypeScript](https://bobbyhadz.com/blog/typescript-http-request-axios)

[Frontend API calls with TypeScript and Axios](https://javascript.plainenglish.io/frontend-api-calls-with-typescript-and-axios-68792d1e63c2)

## 基本寫法

```ts
type User = {
  id: number;
  email: string;
  first_name: string;
};

type GetUsersResponse = {
  data: User[];
};

const { data, status } = await axios.get<GetUsersResponse>(
    'https://reqres.in/api/users',
);
```

這邊的 `GetUsersResponse` 是 call api 回來資料的型別