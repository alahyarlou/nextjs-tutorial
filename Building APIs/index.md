# Building APIs

In general, it is common add a folder named 'api' inside the app folder so that we can add our own routes inside it.

well, first create a folder ```api```

Then, create own route for Example: ``route.js``

## Route

- GET -> getting data
- POST -> creating data
- PUT -> updating data

we first talk about `GET` method:

```js
import { NextResponse } from "next/server";

export function GET(request) {
  return NextResponse.json([
    { id: 1, name: "Mosh" },
    { id: 2, name: "ali" },
  ]);
}
```

## Getting Single Object

Create dynamic route for example: Folder([id])

```js
import { NextRequest } from 'next/server';

export function GET(request,{params}){
  // fetching data from a db
  // If notFound retrun 404 an error
  // else return data

  if(params.id>10)
    return NextRequest.json({error:'User Not Found'},{status:404});

  return NextRequest.json({id:1,name:'Mosh'});
  }
```

## Creating an Object

```js
import { NextRequest } from "next/server";

export async function POST(request) {
  const body = await request.json();

  // Validate
  // If invalid, return 400
  // Else return response data

  if (!body.name)
    return NextRequest.json({ error: "Name is required" }, { status: 400 });

  return NextRequest.json({ id: 1, name: body.name }, { status: 201 });
}
```

## Updating an Object

- validate the request body
- If invalid, return 400
- Fetch the user with the given id
- If doesn't exist, return 404
- Update the user
- Return updated the user

---

```js
import { NextRequest } from 'next/server';

export async function PUT(request,{params}:{params:{id:number}){

  if(!body.name)
    return NextRequest.json({error:'Name is required'},{status:400});

  if(params.id>10)
    return NextRequest.json({error:'User Not Found'},{status:404});

  return NextRequest.json({id:1,name:body.name},{status:200});

  }
```

## Deleting an Object

- Fetch the user from db
- If NotFound , return 404
- Delete the user
- Return 200

---

```js
import { NextRequest } from 'next/server';

export async function DELETE(request,{params}:{params:{id:number}){

  if(params.id>10)
    return NextRequest.json({error:'User Not Found'},{status:404});

  return NextRequest.json({},{status:200});

  }
```

## Validation Request with Zod

you can learn about `zod` in [Zod](https://www.zod.dev) .

first we go into terminal and install zod


```js
npm install zod
```

Then we create file called `schema.js` OR `schema.tsx`

---

```js
import { z } from "zod";

const schema = z.object({
  name: z.string().min(3),
});

export default schema;
```

Now we go back to ouer route file then we import our `schema`.

---

```js
import { NextRequest } from 'next/server';
import schema from './schema';

export async function PUT(request,{params}:{params:{id:number}){
  const validation = schema.safeParse(body);

  if(!validation.success)
    return NextRequest.json(validation.error.errors,{status:400});

  if(params.id>10)
    return NextRequest.json({error:'User Not Found'},{status:404});

  return NextRequest.json({id:1,name:body.name},{status:200});

  }
```
