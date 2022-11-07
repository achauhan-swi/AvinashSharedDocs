*PLTFRS-10003 (Analysis)*
-------------

## Target Ticket:[PLTFRS-10003](https://issues.sierrawireless.com/browse/PLTFRS-10003)

- Goals: 
	- Company admin shall be able to create a Sierra user w/o entering a password
	- Give the possibility to assign users to an AirVantage company.
- Background
	- After SSO feature deployment, when a user is "deleted" from an account it is not actually deleted. It is de-associated from the AirVantage account but still remains as a Sierra Wireless user (for the Source, Legato forum, etc...). The direct consequence was that if for any reason someone wants to give this user access to an AirVantage account, the "Create user" feature won't work because the user already exits. Thus requirement to replace the "Create" feature by an "Invite" came. Besides, this workflow was also recommended for security reasons (user will have to accept the invitation).
	- The motive was to improve the process of adding user to a company so that they can access Sierra Wireless services particularly AirVantage where user needs to be part of a company.

## Parent Issue: [ROADMAP-211](https://issues.sierrawireless.com/browse/ROADMAP-211)

- Provide Brooklyn developers a single sign on experience with Sierra Wireless.
- Link to requirement page: [Requirement](https://confluence.sierrawireless.com/pages/viewpage.action?spaceKey=~DLA&title=Single+Sign+On+%3A+StageGate+1)

## Child Issues: 
### PLTFRS-11348 : [PLTFRS-11348](https://issues.sierrawireless.com/browse/PLTFRS-11348)
- Description:Invite a user to join Sierra Wireless

	> Added /session/invite endpoint, email templates, existing and new user workflows. Email 
	> templates based on the layout from the sign up confirmation emails. For the new user flow 
	>,modified the existing signup so that it would pre-populate the email address, make it 
	> non-editable, and skip the email confirmation since that is done when responding to the invite 
	> email.
- workflow : 
	- calling API to invite an user, providing the email of the user invited, and access rights (based on his role), and the company he is invited to.
	- If the user already exists, then it will be associated to the company he was invited.
	- If the user does not exist, but exists in Sierra SSO, user will be created and associated to the company.
	- If the user does not exists in Sierra SSO, then it will be created in Sierra SSO first, then added to Octave and associated to the company.
	- In all cases, the user email is verified by Sierra SSO.
	- Only admins can send this request.

- components: AuthServer
- MRs
	- authentication-frontend
		- Tech: Spark
		- MR1 : [MR1](https://github.com/AirVantage/authentication-frontend/pull/70/files)
			- commit id: 23bbd46f5ad72c655077c26208cf0d4a2e3d57ea
			- Details of change:
				- class/function :
					- InviteEndPoint is added
					- SignUpEndpoint : buildcallbackUrl function build URL is added

				- Test cases: 
					- TestConfig:new String fields and their default values are added
					- SignupEndpoint 4 integration test cases are added .
					- InviteEndPoint Integration test file is added.
					- AuthServerMock : mock for invitedUserDetails and inviteApiClient is added
	- av-routing
		- MR2 : [MR2](https://github.com/AirVantage/av-routing/pull/53/files)

### PLTFRS-11349 :[PLTFRS-11349](https://issues.sierrawireless.com/browse/PLTFRS-11349)

- Goal : Invite a user to join AirVantage
- Components : Accounts
- *Duplicate*

### PLTFRS-11350 :[PLTFRS-11350](https://issues.sierrawireless.com/browse/PLTFRS-11350)
- Description: Request to join a company
		Closed with comment:"Not in the requirements for the moment"
- Components : AuthServer,Accounts

### PLTFRS-11762 :[PLTFRS-11762](https://issues.sierrawireless.com/browse/PLTFRS-11762)
- Description : Give the possibility to add a different URI from the redirect URI to redirect the user after invitation.Add the possibility to have several redirect URIs
	- MRs
		- authentication-server
			- MR1 :[MR1](https://github.com/AirVantage/authentication-server/pull/138/files)
				- commit Id: 4e07b2a0b9cee75957b3e46fcca9a2ac4f7c5d91
				- Details of change:
					- class/function:
						- UrisDao class is added for handling URI
						- AVOP_API_CLIENT_URIS table is created to hold Redirect_Uri_List
					- Test Files:
						- assertion added for redirectUris in ApiClientPersistIT and ApiClientUpdateIT
			- MR2 :[MR2](https://github.com/AirVantage/authentication-frontend/pull/72/files)



Impt Links:
- [Invite-User-WorkFlow](https://confluence.sierrawireless.com/pages/viewpage.action?spaceKey=AVENG&title=Join+a+Sierra+Wireless+Service)
- [BROOKLYN-Invite-User-Requirement](https://confluence.sierrawireless.com/display/BROOKLYN/Invite+User)

