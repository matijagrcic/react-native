[Localization](https://docs.expo.dev/versions/latest/sdk/localization/)

```jsx
//in .json
{
  "greeting": "Hello, %{name}. Good morning!"
}

i18n.t('greeting', {
  name: 'John'
})
```

[useTranslation (hook)](https://react.i18next.com/latest/usetranslation-hook)

```jsx
const { t, i18n } = useTranslation();

//in .json
{
  "greeting": "Hello, {{name}}. Good morning!"
}

{
  t("greeting", { name: "John" });
}
```
