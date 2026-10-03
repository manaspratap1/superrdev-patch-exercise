## Summary of changes:

1. **Removed artificial API delay:** I noticed the API was very slow on the frontend . I found an intentional `Thread.sleep` block in `TaskContoller` that was blovking the thread based on the search query length. I deleted that code block to make the APi respond quickly not simulating a delay.

2. **Removed in-memory pagination:** I noticed the controller od performing in-memory pagination and fetching all teh task in memory and then filters out the required ones, this causes OutOfMemoryError when the number of rows are in lakhs or millions. I replaced that method by the standard JPA pagination which passes the Pageable object and converts it into standatrd limit and offset query fething only the number of rows required to send in response.
 
3. **Fixed frontend pagination reset bug:** In the UI, if you navigated to page 2 and then applied a filter, it would show an empty table. I updated `App.jsx` to reset the `page` state to 1 whenever the search or status filters are modified.