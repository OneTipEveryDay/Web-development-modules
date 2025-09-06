> many websites use JavaScript APIs to request data from the server and update the page content without a page load. So when the user searches for a new product, the browser only requests the data which is needed to update the page — the set of new books to display, for instance.
>
> <img width="1200" height="570" alt="image" src="https://github.com/user-attachments/assets/a1d0c111-56b3-4ee3-8619-87fc0eb6e9d7" />


The main API here is the Fetch API. This enables JavaScript running in a page to make an HTTP request to a server to retrieve specific resources. When the server provides them, the JavaScript can use the data to update the page, typically by using DOM manipulation APIs. The data requested is often JSON, which is a good format for transferring structured data, but can also be HTML or just text.

## Fetching text content 
...























