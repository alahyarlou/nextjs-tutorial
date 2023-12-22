# Building APIs (Exercises)

## Building Products API

I want you to implement an API for managing products.So when we hit `/api/products`
we get an area of product objects,each product has 3 properties : ID, name, price

## Solution Exercise

so we're going in the `api folder` and add new folder called `products` then we add `route.js` OR `route.tsx` file in thise route.

---

Open the `products/route.js` file and write this code:

```js
import { NextRequest } from "next/server";

export function GET(request) {
  return NextRequest.json([
    { id: 1, name: "Mosh", price: 2.5 },
    { id: 2, name: "Ali", price: 4 },
    { id: 3, name: "Mikle", price: 5.5 },
  ]);
}
```

```js
import { NextRequest } from "next/server";

export async function POST(request) {
  const body = await NextRequest.json();
  //validation of body request data
}
```

Create `products/schema.js` and Open for to write this code:

```js
import { z } from "zod";

const schema = z.object({
  name: string().min(3),
  price: z.number().min(1).max(100),
});
export default schema;
```

So Then we back going the `products/route.js` file:

---

```js
import { NextRequest, NextResponse } from "next/server";
import schema from './schema.js';

export async function POST(request) {
  const body = await NextRequest.json();
  const validation = schema.safeParse(body);

  if (!validation.success){
    return NextResponse.json({ validation.error.errors },{ status:400 });
  }

  return NextResponse.json({ id:10, name:body.name, price:body.price },{ status:201 });
}
```
