# useTheme
React Custom Hook


### Import the necessary components from Material UI:
```jsx
import { createMuiTheme } from '@material-ui/core/styles';
import { ThemeProvider } from '@material-ui/styles';
```


### Create custom light and dark themes with createMuiTheme:
```jsx
const lightTheme = createMuiTheme({
  palette: {
    type: 'light',
    primary: {
      main: '#1976d2',
    },
    secondary: {
      main: '#f50057',
    },
  },
});

const darkTheme = createMuiTheme({
  palette: {
    type: 'dark',
    primary: {
      main: '#90caf9',
    },
    secondary: {
      main: '#f48fb1',
    },
  },
});
```

### Create the useTheme custom hook:
```jsx
import { useState, useEffect } from 'react';

export const useTheme = () => {
  const [theme, setTheme] = useState(lightTheme);

  useEffect(() => {
    // Retrieve the current theme from Local Storage
    const storedTheme = window.localStorage.getItem('theme');
    if (storedTheme) {
      setTheme(JSON.parse(storedTheme));
    }
  }, []);

  useEffect(() => {
    // Store the current theme in Local Storage
    window.localStorage.setItem('theme', JSON.stringify(theme));
  }, [theme]);

  return [theme, setTheme];
};
```

### Use the useTheme custom hook in the application:
```jsx
import { useTheme } from './useTheme';

const App = () => {
  const [theme, setTheme] = useTheme();

  const toggleTheme = () => {
    // Toggle between light and dark themes
    setTheme(theme.palette.type === 'light' ? darkTheme : lightTheme);
  };

  return (
    <ThemeProvider theme={theme}>
      <div className="App">
        <button onClick={toggleTheme}>Toggle theme</button>
        <h1>Material UI app with custom light and dark themes</h1>
      </div>
    </ThemeProvider>
  );
}
```
