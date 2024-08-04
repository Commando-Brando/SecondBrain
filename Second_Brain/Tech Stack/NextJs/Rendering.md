TARGET DECK: TechStack::NextJs

Q: In NextJs what is the default NextJs rendering type for a simple component?
A: Static rendering
<!--ID: 1721653720903-->

END

Q: In NextJs what does NextJs do on the server when serving static pages to serve up faster?
A: It caches static pages on the server 
<!--ID: 1721653720917-->

END

Q: In NextJs how can you turn a plain NextJs component into a dynamic component?
A: To make a NextJs file dynamic you need to have dynamic behavior occur in the file or create the following variable in a component `export const dynamic = "force-dynamic"
<!--ID: 1721653749911-->

END

Q: In NextJs what does putting `"use server";` at the top of a file do?
A: It means you are exposing an endpoint for the client to hit
<!--ID: 1721653720927-->
END

Q: In NextJs what does the following import do? `import "server-only"`
A: It indicates that this file should never run on client-side, only on server
<!--ID: 1721653720933-->

END 

Q: What is the NextJs Image component?
A: A component that extends the HTML `<img>` element with features for automatic image optimization:

- **Size Optimization:** Automatically serve correctly sized images for each device, using modern image formats like WebP and AVIF.
- **Visual Stability:** Prevent [layout shift](https://nextjs.org/learn/seo/web-performance/cls) automatically when images are loading.
- **Faster Page Loads:** Images are only loaded when they enter the viewport using native browser lazy loading, with optional blur-up placeholders.
- **Asset Flexibility:** On-demand image resizing, even for images stored on remote servers

[YouTube Reference](https://www.youtube.com/watch?v=IU_qq_c_lKA)
<!--ID: 1721653720968-->

END

Q: In NextJs what kind of rendering do hooks go in?
A: Client side only because hooks are all about updating state/client things once the page is on the client's device
<!--ID: 1721654049056-->

END

