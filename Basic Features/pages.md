---
description: Next.js pages are React Components exported in a file in the pages directory. Learn how they work here.
---

# Pages

Next.js에서의 **페이지**는 `pages` 폴더 내부에 있는 `.js`, `.jsx`, `.ts`, 또는 `.tsx` 리액트 컴포넌트 파일을 뜻합니다. 모든 페이지는 파일 명에 따라 루트 명이 정해집니다.

**예시**: `pages/about.js`라는 파일을 만들게 되면, 다음과 같은 리액트 컴포넌트를 내보내게 되고, 이는 `/about`이라는 루트를 통해 접근 가능해집니다.

```jsx
function About() {
  return <div>About</div>
}

export default About
```

### 동적 루트를 가진 페이지들 

Next.js는 동적 루트 생성이 가능합니다. 예를 들어 `pages/posts/[id].js`를 생성하게 되면, `posts/1`, `posts/2` 등의 루트로 접근 가능합니다. 

> 동적 루트에 대한 더욱 자세한 내용은, [Dynamic Routing documentation](/docs/routing/dynamic-routes.md)를 참고할 수 있습니다.

## Pre-rendering (프리 렌더링)

Next.js는 모든 페이지를 프리 렌더(pre-render)합니다. 기존 자바스크립트의 CSR 방식이 아닌 모든 페이지에 대한 HTML을 먼저 생성함으로서 접근성(SEO)과 퍼포먼스의 측면에서 더욱 나은 결과를 가져옵니다.

생성된 모든 HTML은 최소한의 자바스크립트 코드로 이루어지며, 브라우저에 의해 페이지가 로딩되면, 상호작용을 위한 자바스크립트 코드가 실행됩니다. (해당 과정을 _hydration_ 이라고 부릅니다.) 

### Pre-rendering(프리 렌더링)의 두 가지 방법

Next.js는 두 가지 형태로 프리 렌더링을 진행합니다: **Static Generation(정적 생성)** 그리고 **Server-side Rendering(서버 사이드 렌더링)**. 두 방식은 **언제** HTML이 생성되는 시점에 있어 차이점을 가집니다. 

- [**Static Generation(정적 생성) (권장)**](#static-generation-recommended): HTML이 **build time(빌드 타임)** 에 생성되며, 요청에 따라 재사용 됩니다.
- [**Server-side Rendering(서버 사이드 렌더링)**](#server-side-rendering): **요청이 들어올 때마다** HTML이 생성됩니다.

Next.js는 각 페이지에 대해 어떤 프리 렌더링 방법을 사용할 것인지에 대한 **선택지**를 제공합니다. 즉, 대부분의 페이지를 Static Generation(정적 생성)으로 제작하고, 몇몇 페이지를 Server-side Rendering(서버 사이드 렌더링)으로 제작하여 하이브리드(hybrid)Next.js 앱을 만들 수 있다는 의미기이도 합니다. 


퍼포먼스의 측면에서 Server-side Rendering(서버 사이드 렌더링) 보다 **Static Generation(정적 생성)** 을 권장합니다. 정적으로 생성된 페이지들은 성능을 향상시키기 위해 추가 구성되지 않고도 CDN에 캐시됩니다. 그러나 경우에 따라 Server-side Rendering (서버사이드 렌더링)이 유일한 선택지가 될 수 있습니다. 

Static Generation 그리고 Server-side Rendering과 더불어 **Client-side Rendering(클라이언트 사이드 렌더링)** 을 사용할 수 있습니다. 이는 페이지의 일부를 오직 클라이언트 측의 자바스크립트 코드로 렌더할 수 있다는 것을 의미합니다. 더욱 자세한 내용은 [Data Fetching](/docs/basic-features/data-fetching/client-side.md) 을 참고할 수 있습니다.

## Static Generation (권장)

<details open>
  <summary><b>예시</b></summary>
  <ul>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-wordpress">WordPress Example</a> (<a href="https://next-blog-wordpress.vercel.app">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/blog-starter">Blog Starter using markdown files</a> (<a href="https://next-blog-starter.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-datocms">DatoCMS Example</a> (<a href="https://next-blog-datocms.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-takeshape">TakeShape Example</a> (<a href="https://next-blog-takeshape.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-sanity">Sanity Example</a> (<a href="https://next-blog-sanity.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-prismic">Prismic Example</a> (<a href="https://next-blog-prismic.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-contentful">Contentful Example</a> (<a href="https://next-blog-contentful.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-strapi">Strapi Example</a> (<a href="https://next-blog-strapi.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-prepr">Prepr Example</a> (<a href="https://next-blog-prepr.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-agilitycms">Agility CMS Example</a> (<a href="https://next-blog-agilitycms.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-cosmic">Cosmic Example</a> (<a href="https://next-blog-cosmic.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-buttercms">ButterCMS Example</a> (<a href="https://next-blog-buttercms.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-storyblok">Storyblok Example</a> (<a href="https://next-blog-storyblok.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-graphcms">GraphCMS Example</a> (<a href="https://next-blog-graphcms.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-kontent">Kontent Example</a> (<a href="https://next-blog-kontent.vercel.app/">Demo</a>)</li>
    <li><a href="https://github.com/vercel/next.js/tree/canary/examples/cms-builder-io">Builder.io Example</a> (<a href="https://cms-builder-io.vercel.app/">Demo</a>)</li>
    <li><a href="https://static-tweet.vercel.app/">Static Tweet (Demo)</a></li>
  </ul>
</details>

**Static Generation**을 사용한 페이지는 **빌드 타임**에 HTML이 생성됩니다. 제작의 시점, 즉 명령어인 `next build`의 실행과 동시에 페이지의 HTML이 생성됩니다. 각각의 요청에 따라 해당 HTML은 재사용되며, CDN에 캐시됩니다.

Next.js에서는 **데이터의 유무와는 상관없이** 정적으로 페이지 생성이 가능합니다. 아래 다양한 케이스를 살펴봅시다. 

### 데이터가 없을때의 Static Generation 

Next.js는 Static Generation을 통해 페이지를 데이터를 가져오지 않은 상태에서도 프리 렌더링을 진행합니다. 예시를 살펴봅시다:  

```jsx
function About() {
  return <div>About</div>
}

export default About
```

위 페이지는 프리 렌더링을 위해 외부 데이터를 필요로 하지 않습니다. 이러한 경우, Next.js는 빌드 타임 중 페이지당 하나의 HTML 파일을 생성합니다.  

### 데이터가 있을때의 Static Generation

몇몇 페이지들은 프리 렌더링을 위해 외부 데이터를 필요로 합니다. 두 가지의 경우가 있는데, 한 가지, 또는 두 가지에 모두 해당될 수 있습니다. 다음의 Next.js 함수를 적용할 수 있습니다: 

1. 페이지의 **content(내용)**이 외부 데이터에 의존할 때:  `getStaticProps`를 사용.
2. 페이지의 **paths(경로)**가 외부 데이터에 의존할 때: `getStaticPaths`를 사용(보편적으로 `getStaticProps`와 함께 사용).

#### 시나리오 1: 페이지의 **content(내용)** 이 외부 데이터에 의존할 때 

**예시**: CMS(content management system)로 부터 블로그의 포스팅 내용을 블로그 페이지로 가져올 때.   

```jsx
// TODO: 해당 페이지가 프리 렌더링 되기 전, 
//       API endpoint를 활용하여 `posts` 가져오기 
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

export default Blog
```

프리 렌더링 시점에 해당 데이터를 불러오기(fetch)위해, 같은 파일 내 내보내기(export)가 가능한 `async` 함수, `getStaticProps` 활용할 수 있습니다. 해당 함수는 빌드 타임에 호출되며, 프리 렌더 시 가져온 데이터를 페이지 내 `props`로 전달 할 수 있도록 합니다.

```jsx
function Blog({ posts }) {
  // 블로그 포스트들을 렌더합니다
}

// 아래 함수는 빌드타임에 호출됩니다
export async function getStaticProps() {
  // 외부 API endpoint를 호출하여 포스트 데이터를 가져옵니다  
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // { props: { posts } }를 리턴하여 Blog 컴포넌트가 
  // 빌드 타임 시점에 `posts` 를 prop으로 받을 수 있도록 합니다
  return {
    props: {
      posts,
    },
  }
}

export default Blog
```

 `getStaticProps` 함수가 어떻게 작동하는지에 대한 더욱 자세한 내용은 [Data Fetching documentation](/docs/basic-features/data-fetching/get-static-props.md)을 참고할 수 있습니다.

#### 시나리오 2: Your page paths depend on external data

Next.js allows you to create pages with **dynamic routes**. For example, you can create a file called `pages/posts/[id].js` to show a single blog post based on `id`. This will allow you to show a blog post with `id: 1` when you access `posts/1`.

> To learn more about dynamic routing, check the [Dynamic Routing documentation](/docs/routing/dynamic-routes.md).

However, which `id` you want to pre-render at build time might depend on external data.

**Example**: suppose that you've only added one blog post (with `id: 1`) to the database. In this case, you'd only want to pre-render `posts/1` at build time.

Later, you might add the second post with `id: 2`. Then you'd want to pre-render `posts/2` as well.

So your page **paths** that are pre-rendered depend on external data**.** To handle this, Next.js lets you `export` an `async` function called `getStaticPaths` from a dynamic page (`pages/posts/[id].js` in this case). This function gets called at build time and lets you specify which paths you want to pre-render.

```jsx
// This function gets called at build time
export async function getStaticPaths() {
  // Call an external API endpoint to get posts
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // Get the paths we want to pre-render based on posts
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))

  // We'll pre-render only these paths at build time.
  // { fallback: false } means other routes should 404.
  return { paths, fallback: false }
}
```

Also in `pages/posts/[id].js`, you need to export `getStaticProps` so that you can fetch the data about the post with this `id` and use it to pre-render the page:

```jsx
function Post({ post }) {
  // Render post...
}

export async function getStaticPaths() {
  // ...
}

// This also gets called at build time
export async function getStaticProps({ params }) {
  // params contains the post `id`.
  // If the route is like /posts/1, then params.id is 1
  const res = await fetch(`https://.../posts/${params.id}`)
  const post = await res.json()

  // Pass post data to the page via props
  return { props: { post } }
}

export default Post
```

To learn more about how `getStaticPaths` works, check out the [Data Fetching documentation](/docs/basic-features/data-fetching/get-static-paths.md).

### When should I use Static Generation?

We recommend using **Static Generation** (with and without data) whenever possible because your page can be built once and served by CDN, which makes it much faster than having a server render the page on every request.

You can use Static Generation for many types of pages, including:

- Marketing pages
- Blog posts and portfolios
- E-commerce product listings
- Help and documentation

You should ask yourself: "Can I pre-render this page **ahead** of a user's request?" If the answer is yes, then you should choose Static Generation.

On the other hand, Static Generation is **not** a good idea if you cannot pre-render a page ahead of a user's request. Maybe your page shows frequently updated data, and the page content changes on every request.

In cases like this, you can do one of the following:

- Use Static Generation with **Client-side Rendering:** You can skip pre-rendering some parts of a page and then use client-side JavaScript to populate them. To learn more about this approach, check out the [Data Fetching documentation](/docs/basic-features/data-fetching/client-side.md).
- Use **Server-Side Rendering:** Next.js pre-renders a page on each request. It will be slower because the page cannot be cached by a CDN, but the pre-rendered page will always be up-to-date. We'll talk about this approach below.

## Server-side Rendering

> Also referred to as "SSR" or "Dynamic Rendering".

If a page uses **Server-side Rendering**, the page HTML is generated on **each request**.

To use Server-side Rendering for a page, you need to `export` an `async` function called `getServerSideProps`. This function will be called by the server on every request.

For example, suppose that your page needs to pre-render frequently updated data (fetched from an external API). You can write `getServerSideProps` which fetches this data and passes it to `Page` like below:

```jsx
function Page({ data }) {
  // Render data...
}

// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page via props
  return { props: { data } }
}

export default Page
```

As you can see, `getServerSideProps` is similar to `getStaticProps`, but the difference is that `getServerSideProps` is run on every request instead of on build time.

To learn more about how `getServerSideProps` works, check out our [Data Fetching documentation](/docs/basic-features/data-fetching/get-server-side-props.md)

## Summary

We've discussed two forms of pre-rendering for Next.js.

- **Static Generation (Recommended):** The HTML is generated at **build time** and will be reused on each request. To make a page use Static Generation, either export the page component, or export `getStaticProps` (and `getStaticPaths` if necessary). It's great for pages that can be pre-rendered ahead of a user's request. You can also use it with Client-side Rendering to bring in additional data.
- **Server-side Rendering:** The HTML is generated on **each request**. To make a page use Server-side Rendering, export `getServerSideProps`. Because Server-side Rendering results in slower performance than Static Generation, use this only if absolutely necessary.

## Learn more

We recommend you to read the following sections next:

<div class="card">
  <a href="/docs/basic-features/data-fetching/overview.md">
    <b>Data Fetching:</b>
    <small>Learn more about data fetching in Next.js.</small>
  </a>
</div>

<div class="card">
  <a href="/docs/advanced-features/preview-mode.md">
    <b>Preview Mode:</b>
    <small>Learn more about the preview mode in Next.js.</small>
  </a>
</div>

<div class="card">
  <a href="/docs/routing/introduction.md">
    <b>Routing:</b>
    <small>Learn more about routing in Next.js.</small>
  </a>
</div>

<div class="card">
  <a href="/docs/basic-features/typescript.md#pages">
    <b>TypeScript:</b>
    <small>Add TypeScript to your pages.</small>
  </a>
</div>
