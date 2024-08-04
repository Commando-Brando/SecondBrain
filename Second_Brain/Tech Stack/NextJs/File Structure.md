TARGET DECK: TechStack::NextJs
# Notes

# Flashcards

Q: In NextJs what does prepending a directory with an underscore do?
A: It tells page router not to include the file in the routing
<!--ID: 1721653720997-->

Q: How can the NextJs Image component cause an increase in Vercel costs?
A: The image optimizations cause a lot of image updates with different resolutions which increase the amount of images being pulled from back-end which increase image costs. There are a certain amount free.
<!--ID: 1721654011901-->

END

Q: When using the NextJs Image component why do you need to whitelist hostname's of where to accept images from?
A: If not user's can retrieve any image they want on the web which would increase costs and pose a security risk. Specifying in the NextJs config the hostname patterns resolves this.

![[NextImageConfig.png]]
<!--ID: 1721654011905-->

END

Example: Imagine you click on an image and it opens in a modal. Then if you refresh the page instead of losing where you were it could take you to a standalone page for that image.
<!--ID: 1721654011908-->

END

Q: For NextJs parallel routes what are the steps to setting it up?
A: 
- Add modal prop to route layout and pass in like children
- Create `@modal` directory
- Put add `default.tsx` module
- Add another route, example (.)photos/[id]
- Add what to render here, should be modal but can be anything like a div
- Now you can use `Link` component to route to that page and it with render modal
<!--ID: 1721653720992-->

END
