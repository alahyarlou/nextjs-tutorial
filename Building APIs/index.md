# Building APIs

In general, it is common add a folder named 'api' inside the app folder so that we can add our own routes inside it.

well, first create a folder -> api

then, create own route for Example: route.js

## Route

- GET -> getting data
- POST -> creating data
- PUT -> updating data

we first talk about `GET` method:

```bash
import {NextResponse} from 'next/server'

export function GET(request){
    return NextResponse.json([
    {id:1,name:'Mosh'},
    {id:2,name:'ali'}
    ])
  }
```

## Getting Single Object

create dynamic route for example: Folder([id])

```bash
import {NextRequest} from 'next/server'

export function GET(request,{params}:{params:{id:number}){
    // fetching data from a db
    // If notFound retrun 404 an error
    // else return data
  }
```
