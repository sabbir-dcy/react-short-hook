# react-short-hook

google authentication hooks for reset password only. **testing purpose**.

#Installation

```bash
# with npm
npm i react-short-hook

# with yarn
yarn add react-short-hook
```

- [usePassResetEmail](#usePassResetEmail)

## usePassResetEmail

### parameter:

- auth: Auth instance for the app

### returns:

- `sendPassResetEmail(email: string)` function to send the email.
- `loading` returns boolean that indicates processing state while sending the email.
- `error` returns error if any error occurs. usecase: `error.message` or `error.toast`
- `sent` returns boolean if the email has sent successfully without any error.

```js
// import package
import { usePassResetEmail } from 'react-short-hook';
```

```js
const [sendPassResetEmail, loading, error, sent] = usePassResetEmail(auth);
```

## example code

```js
function resetUserPassword() {
  const [sendPassResetEmail, loading, error, sent] = usePassResetEmail(auth);

  useEffect(() => {
    error && console.log(error.toast);
    sent && console.log('email sent successfully');
  }, [error, sent]);

  if (loading) return <p>sending in progress</p>;

  const emailRef = useRef();
  const handleResetPassword = () => {
    sendPassResetEmail(emailRef.current.value);
  };
  return (
    <div className="App">
      <input type="email" name="email" ref={emailRef} />
      <button onClick={handleResetPassword}>send</button>
    </div>
  );
}
```
