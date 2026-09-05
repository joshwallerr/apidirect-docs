# Team Accounts

Share one API Direct account with your team. Everyone you invite works inside the same account: the same API keys, the same usage, the same bill. Manage your team from the [Team section in Settings](https://apidirect.io/dashboard/settings).

## How Accounts Work

Every user has an account of their own, created when they sign up. An account holds the API keys, usage history, credit and billing details. Inviting someone gives them access to your account; it does not create anything new for them.

One person can belong to several accounts. The account menu at the bottom of the dashboard sidebar switches between them. Everything on the dashboard, including the Playground, applies to the account you have selected.

## Roles

Each member has one of three roles in an account.

| | Member | Admin | Owner |
|---|:---:|:---:|:---:|
| View usage and spend | ✓ | ✓ | ✓ |
| View API keys | ✓ | ✓ | ✓ |
| Create and revoke API keys | | ✓ | ✓ |
| Run requests in the Playground | | ✓ | ✓ |
| View billing and spending limits | | ✓ | ✓ |
| Change payment method and spending limits | | | ✓ |
| Invite and remove members | | ✓ | ✓ |
| Add or remove owners | | | ✓ |
| Rename the account | | | ✓ |

**Member** is read-only. Members can see how the account is being used and which keys exist, but cannot create keys or run Playground requests, because both spend the account's money. The Billing page is not available to members.

**Admin** runs the team day to day: keys, the Playground and the member list. Admins cannot change billing and cannot promote, demote or remove an owner.

**Owner** can do everything, including billing and managing other owners. The person who created the account is always an owner and cannot be demoted, removed, or leave.

## Inviting Someone

1. Go to [Dashboard > Settings](https://apidirect.io/dashboard/settings) and find the Team section
2. Enter their email address and choose a role
3. Click "Send invite"

They receive an email with a link. The link only works when they are signed in with the invited address, and it expires after **14 days**. Owners and admins can invite; only an owner can invite someone as an owner.

Sending a second invitation to the same address replaces the first one, so the older link stops working. Pending invitations can be cancelled from the Team section at any time.

## Accepting an Invitation

Open the link in the invitation email. If you do not have an API Direct account yet, sign up with the invited email address and you will be brought back to the invitation. If you are signed in with a different address, sign out and sign back in with the invited one.

If you signed up because you were invited, you join the inviting account and no separate account is created for you. You can create your own account later from the account menu.

## API Keys and Billing

API keys belong to the account, not to the person who created them. A key keeps working when that person leaves, and every request made with it is billed to the account. The limit of 10 keys applies per account.

Playground requests are billed to the account you have selected in the sidebar, whoever runs them.

## Changing Roles and Removing Members

Owners can change anyone's role except the account creator's. Admins can change roles between Member and Admin. Nobody can change their own role.

Removing someone ends their access immediately. Keys they created stay with the account. Anyone other than the account creator can leave an account from the Danger Zone in Settings.

## Deleting an Account

Only the account creator can delete an account, from the Danger Zone in Settings. Deleting an account removes every member's access along with the keys and history. Deletion is refused while other members remain, so remove them first.
