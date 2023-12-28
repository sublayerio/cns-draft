# Create Next Startup - Draft v1

## supervision
A supervisor-endowed user can initiate a session on behalf of a specific user.

This offers **multiple advantages**:

- The supervisor can experience the application from the perspective of the designated user, with visibility constraints based on the user's role, and can execute actions in their stead.
    - This is particularly useful for a supervisor who wants to understand the user experience of those with different roles within the application, without contaminating the logs with unintended login data.
    - It also empowers the supervisor to intervene on behalf of a user who may be struggling with certain actions.
- Logs are enriched with supplementary data indicating that requests were executed under supervisory oversight.


## developer mode

Developer mode can be triggered by `⌘J`. 

![Screenshot 2023-08-09 at 10 52 18](https://github.com/sublayerio/cns-draft/assets/44947294/1fc258ea-aed3-4af6-8dd9-dfcbed10fe92)

Within code `developerMode` can be accessed using the `useDeveloperMode` hook and certain elements or functionality be toggled:

```jsx
import { DeveloperMode } from '@/library/developer-mode'

export default function App() {

	return (
		<div>
			<h1>Application</h1>
			<div>
				{testMode ? (
					<div>
						Show this in developer mode
					</div>
				) : null}
			</div>
		<div>
	)
}
```

## events

```json
{
	"changes": {
		"order_reference" : {
			"prev" : "V23066",
			"next" : "903272",
			"userId" : "user::john",
			"supervisorId" : "user::sublayerio",
			"operation" : "change",
			"source" : "user",
			"type" : "text",
			"time" : "2023-03-26T20:09:26.139"
		},
		"name" : {
			"prev" : null,
			"next" : "903272 Volkswagen Polo G527JT",
			"userId" : "user::john",
			"supervisorId" : "user::sublayerio",
			"operation" : "change",
			"source" : "formula",
			"type" : "text",
			"time" : "2023-03-26T20:09:26.141"
		}
	}
}
```


- `source`: can be of the following values
	- `formula`: a change originating from formula middleware, the computed value has changed compared to the previously stored value.
	- `user`: a change originating from a call to `updateRecords` by a user, either through the client side application or an external service (which is also a user).
- `prev`: the previous value, `null` when empty.
- `userId`: the ID of the user that has made the change.
- `supervisorId`: the ID of the user under which supervision the change was made.
