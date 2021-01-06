# Projeto React Native com typescript

- Backend: [Ambiente avançado](https://github.com/mrcarromesa/gostack-gobarber-ts-arquitetura2)

- Iniciando o projeto:

```bash
npx react-native init appgobarber --template react-native-template-typescript
```

- Abrir o projeto no vscode

- Criar o arquivo `src/App.tsx` com o básico:

```tsx
import React from 'react';
import { View } from 'react-native';

const App: React.FC = () => {
  return <View />;
}

export default App;
```

- Removemos o arquivo `/App.tsx`

- Ajustamos o arquivo `index.tsx`:

```tsx
/**
 * @format
 */

import {AppRegistry} from 'react-native';
import App from './src/App';
import {name as appName} from './app.json';

AppRegistry.registerComponent(appName, () => App);

```

- Podemos remover também as configurações padrões do:
  - eslintrc.js
  - .prettierrc.js

- Criar o arquivo `.editorconfig` com o conteúdo:

```yml
root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
end_of_line = lf
```

---

## ESLint

- Instalar o eslint:

```bash
yarn add eslint@6.8.0 -D
```

- Configurar o eslint:

```bash
yarn eslint --init
```

- Responder:

```bash
How would you like to use ESLint?
```

```bash
To check syntax, find problems, and enforce code style
```

```bash
What type of modules does your project use?
```

```bash
JavaScript modules (import/export)
```

```bash
Which framework does your project use?
```

```bash
React
```

```bash
Does your project use TypeScript?
```

```bash
y
```

```bash
Where does your code run?
```

**Desmarcar todos**

```bash
How would you like to define a style for your project?
```

```bash
Use a popular style guide
```

```bash
Which style guide do you want to follow?
```

```bash
Airbnb: https://github.com/airbnb/javascript
```

```bash
What format do you want your config file to be in?
```

```bash
JSON
```

```bash
Would you like to install them now with npm?
```

```bash
Y
```

- Após instalar remover o arquivo `package-look.json`

- Executar o comando:

```bash
yarn
```

- Para garantir que a versão do eslint foi instalada a correta, executar o comando:

```bash
yarn add eslint@6.8.0 -D
```

- Criar o arquivo `.eslintignore`:

```yml
**/*.js
node_modules
build
```

- O arquivo `.eslintrc.js` inserir o seguinte conteúdo:

```js
module.exports = {
  env: {
    es6: true,
    jest: true,
  },

  extends: [
    'airbnb',
    'eslint:recommended',
    'prettier',
    'prettier/react',
    'plugin:import/errors',
    'plugin:import/warnings',
    'plugin:import/typescript',
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
    'prettier/@typescript-eslint',
    'plugin:prettier/recommended',
  ],

  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2020,
    sourceType: 'module',
  },
  plugins: ['react', 'jsx-a11y', 'import', 'react-hooks', 'prettier'],

  rules: {
    'prettier/prettier': 'error',
    'jsx-a11y/label-has-associated-control': 'off',

    'import/prefer-default-export': 'off',
    'no-unused-vars': ['warn', { argsIgnorePattern: '^_' }],
    // 'no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
    'react/jsx-one-expression-per-line': 'off',
    'global-require': 'off',
    'react-native/no-raw-text': 'off',
    'no-param-reassign': 'off',
    'no-underscore-dangle': 'off',
    camelcase: 'off',
    'no-console': ['error', { allow: ['tron'] }],
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
    'import/no-unresolved': 'off',
    'react/prop-types': 'off',
    'react/jsx-props-no-spreading': 'off',

    'import/extensions': ['error', 'never', {"png": "always"}],
    '@typescript-eslint/explicit-function-return-type': 'off',
    'react/jsx-filename-extension': [
      1,
      { extensions: ['.js', '.jsx', '.ts', '.tsx'] },
    ],

    '@typescript-eslint/no-explicit-any': 'off',
    '@typescript-eslint/no-parameter-properties': 'off',
    '@typescript-eslint/no-unused-vars': [
      1,
      { argsIgnorePattern: '^_', varsIgnorePattern: '^ignored?$' },
    ],
    'jsx-a11y/accessible-emoji': 'off',
    '@typescript-eslint/no-empty-function': 'off',
    'no-unused-expressions': 'off',
  },
  settings: {
    'import/resolver': {
      'babel-plugin-root-import': {
        rootPathPrefix: '~/*',
        rootPathSuffix: 'src/*',
      },
      node: {
        extensions: ['.js', '.jsx', '.ts', '.tsx', '.json'],
      },
    },
  },
};

```

- Talvez para funcionar o ESLint no vscode seja necessário dar alguma permissão especial, verificar se não há nenhuma restrição na parte inferior direita da tela.

---

## Prettier

- Instalação:

```bash
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

- Criar o arquivo `prettierrc.js`:

```js
module.exports = {
  "singleQuote": true,
  "trailingComman": "es5",
  "arrowParens": "avoid",
};
```

---

## Babel root import

- Instalar:

```bash
yarn add babel-plugin-root-import eslint-import-resolver-babel-plugin-root-import -D
```

- Ajustar o arquivo `.babel.config.js`

```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['module:metro-react-native-babel-preset'],
    plugins: [
      [
        'babel-plugin-root-import',
        {
          paths: [
            {
              rootPathSuffix: './src/',
              rootPathPrefix: '~/',
            },
          ],
        },
      ],
    ],
  };
};

```

- Ajustar o arquivo `tsconfig.json`:

```json

{
  "compilerOptions": {
    /* Basic Options */
    "target": "esnext",                       /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018' or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    "lib": ["es6"],                           /* Specify library files to be included in the compilation. */
    "allowJs": true,                          /* Allow javascript files to be compiled. */
    // "checkJs": true,                       /* Report errors in .js files. */
    "jsx": "react-native",                    /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    // "sourceMap": true,                     /* Generates corresponding '.map' file. */
    // "outFile": "./",                       /* Concatenate and emit output to single file. */
    // "outDir": "./",                        /* Redirect output structure to the directory. */
    // "rootDir": "./",                       /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
    // "removeComments": true,                /* Do not emit comments to output. */
    "noEmit": true,                           /* Do not emit outputs. */
    // "incremental": true,                   /* Enable incremental compilation */
    // "importHelpers": true,                 /* Import emit helpers from 'tslib'. */
    // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    "isolatedModules": true,                  /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                 /* Raise error on expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,              /* Enable strict null checks. */
    // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    // "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
    // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    // "noUnusedLocals": true,                /* Report errors on unused locals. */
    // "noUnusedParameters": true,            /* Report errors on unused parameters. */
    // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */

    /* Module Resolution Options */
    "moduleResolution": "node",               /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
    "baseUrl": ".",                       /* Base directory to resolve non-absolute module names. */
    "paths": {
      "~/*": ["src/*"]
    },                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
    // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
    // "typeRoots": [],                       /* List of folders to include type definitions from. */
    // "types": [],                           /* Type declaration files to be included in compilation. */
    "allowSyntheticDefaultImports": true,     /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true                   /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */

    /* Source Map Options */
    // "sourceRoot": "./",                    /* Specify the location where debugger should locate TypeScript files instead of source locations. */
    // "mapRoot": "./",                       /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
    // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */

    /* Experimental Options */
    // "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
    // "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */
  },
  "exclude": [
    "node_modules", "babel.config.js", "metro.config.js", "jest.config.js"
  ]
}

```

---

## Reactotron

- Instale as seguintes dependencias:

```bash
yarn add reactotron-react-native reactotron-redux reactotron-redux-saga
```

```bash
yarn add redux redux-saga react-redux
```

- Crie o arquivo `src/config/ReactotronConfig.ts`

- Inicialmente adicionamos o seguinte conteúdo:

```js
import Reactotron from 'reactotron-react-native';
import { reactotronRedux } from 'reactotron-redux';
import sagaPlugin from 'reactotron-redux-saga';

declare global {
  interface Console {
    tron: any;
  }
}

if (__DEV__) {
  const tron = Reactotron.configure()
    .useReactNative()
    .use(reactotronRedux())
    .use(sagaPlugin({ except: [''] }))
    .connect();

  if (tron && tron.clear) {
    tron.clear();
  }

  console.tron = tron;
}


```

- Ajustamos no arquivo `src/App.tsx` é melhor adicionar antes da rota para conseguirmos adicionar o console.tron em mais lugares da aplicação

```js
import './config/ReactotronConfig';
```


---

## Status Bar

- Componente que permite estilizar a Statusbar do dispositivo com a aplicação aberta:

```tsx
<StatusBar barStyle="light-content" backgroundColor="#312e38" />
```

- Algumas propriedades se aplicam apenas a android, como no caso do backgroundColor
- Podemos estilizar por página a status bar.

---

## Styled Components

- Instalar:

```bash
yarn add styled-components
```

- Instalar os types também como dependencia de desenvolvimento:

```bash
yarn add @types/styled-components -D
```

- Criar páginas: `src/pages/SignIn` e `src/pages/SignUp`

- Criar o arquivo de rotas: `src/routes/index.tsx`

- Intalar as dependencias:

```bash
yarn add @react-navigation/native
```

```bash
yarn add react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

- acessar a pasta `ios` e executar o comando:

```bash
pod install
```

- Na maioria dos projetos utilizamos navegação por stack dessa forma podemos utilizar essa opção [Hello React Navigation](https://reactnavigation.org/docs/hello-react-navigation)

- Só precisamos intalar:

```bash
yarn add @react-navigation/stack
```

- Dessa feita podemos partir para `src/route/index.tsx`:

```tsx
import React from 'react';
import { createStackNavigator } from '@react-navigation/stack';

import SignIn from '~/pages/SignIn';
import SignUp from '~/pages/SignUp';

const Auth = createStackNavigator();

const AuthRoutes: React.FC = () => {
  return (
    <Auth.Navigator
      screenOptions={{
        headerShown: false,
        cardStyle: {
          backgroundColor: '#312e38',
        },
      }}
    >
      <Auth.Screen name="SignIn" component={SignIn} />
      <Auth.Screen name="SignUp" component={SignUp} />
    </Auth.Navigator>
  );
};

export default AuthRoutes;

```

- Como nessa aplicação não utilizamos o header colocamos isso no `screenOptions`, essa parte de header é bem costumizavel. Também adicionamos um backgroundColor no Auth.Navigator.

- Por fim no arquivo `src/App.tsx` adicionamos as rotas:

```tsx

import 'react-native-gesture-handler';
import React from 'react';
import { View, StatusBar } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import Routes from '~/routes';

const App: React.FC = () => {
  return (
    <NavigationContainer>
      <StatusBar barStyle="light-content" backgroundColor="#312e38" />
      <View style={{ flex: 1, backgroundColor: '#312e38' }}>
        <Routes />
      </View>
    </NavigationContainer>
  );
};

export default App;

```


- Algo importante é que o `NavigationContainer` precisa ficar por volta das rotas para conseguirmos realizar a navegação.

- Para utilizar imagens .png na aplicação com typescript, criamos o arquivo `src/@types/index.d.ts`:

```ts
declare module '*.png';

```


---

## Importar fontes no React native

- Primeiro de tudo escolher quais fontes serão utilizadas, depois é necessário baixa-las.
- Na raiz do projeto criar uma pasta chamada `assets/fonts/` e colar as fontes baixadas, não confundir com `src/assets/`

**Atenção**
- No android o font-family que utilizaremos para chamar essas fonts é o mesmo nome do arquivo
- No ios o font-family que utilizaremos é diferente... para saber qual nome utilizar, precisamos:
  - Instalar a font no macos
  - Abrir o catalogo de fonts `font book`
  - Escolher no botão (i) na parte superior esquerda da janela para obter as informações da fonte
  - O nome que será utilizado no font-family será o que está em `PostScript name`
**/Atenção**

- Dessa forma o recomendado a fazer é sempre que necessário renomear o nome da fonte para o mesmo nome que está em `PostScript name`, mantendo a extensão do arquivo, pelo menos fica igual tanto para ios e android.

- Na raiz do projeto criar o arquivo `react-native.config.js`:

```js
module.exports = {
  project: {
    ios: {},
    android: {},
  },
  assets: [
    './assets/fonts/',
  ]
}

```

- adicionamos o endereço da pasta onde estão as fonts.


- Por fim executamos o comando:

```bash
yarn react-native link
```

- Após isso como sabemos que foi feito com sucesso o processo?
- Na pasta `android/app/src/main/` deve ter sido copiada a pasta `assets/fonts`
- No arquivo `ios/NOME_PROJETO/info.plist` deve ser adicionado o nome das fonts

- Por fim no style do component adicionar o seguinte:

```ts
export const Title = styled.Text`
  font-family: 'RobotoSlab-Medium'; ${/* <- Nome do font family */}
  font-size: 24px;
  color: #f4ede8;
  margin: 64px 0 24px;
`;
```

---

- Nos componentes criados `src/components/Button` e `src/components/Input` foi criado interface que extends de interface padrão do React Native, só conferir, é bem simpes...


---

- Instalação dos icones no react native:

```bash
yarn add react-native-vector-icons
```

```bash
yarn add @types/react-native-vector-icons -D
```

- Acessar a pasta ios e executar o comando:

```bash
pod install
```

- E no arquivo `ios/NOME_DO_PROJETO/Info.plist` adcionar a(s) fonte(s) de icones que precisamos utilizar:

```xml
<key>UIAppFonts</key>
	<array>
		<string>RobotoSlab-Medium.ttf</string>
		<string>RobotoSlab-Regular.ttf</string>
		<string>Feather.ttf</string>
	</array>
```

- E no arquivo `android/app/build.gradle` no final do arquivo adicionar:

```gradle
project.ext.vectoricons = [
    iconFontNames: [ 'MaterialIcons.ttf', 'EvilIcons.ttf' ] // Name of the font files you want to copy
]

apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
```

- Um exemplo de como utilizar o vector icons: `src/components/Input/index.tsx` e `src/components/Input/styles.ts`

---

### helpers iPhone X

- Nos iPhones X possuem algumas particularidades como no caso a barra superior e o botão virtual home, o qual nos estilos precisamos calcular eles para não ter problemas de usabilidade.

- Para isso podemos utilizar a lib:

```bash
yarn add react-native-iphone-x-helper
```

- Um exemplo de como utilizar está em `src/pages/SignIn/styles.ts`

---

## Usabiliade com o teclado

- Para o teclado não ficar por cima do input quando está aberto, podemos fazer da seguinte forma, conforme em `src/pages/SignIn/styles.ts`

```tsx
// ...
import {
  Image,
  View,
  KeyboardAvoidingView,
  Platform,
  ScrollView,
} from 'react-native';

// ...

return (
    <>
      <KeyboardAvoidingView
        style={{ flex: 1 }}
        behavior={Platform.OS === 'ios' ? 'padding' : undefined}
        enabled
      >
        <ScrollView
          keyboardShouldPersistTaps="handled"
          contentContainerStyle={{ flex: 1 }}
        >
          <Container>
            <Image source={logo} />
            <View>
              <Title>Faça seu logon</Title>
            </View>

            <Input name="email" icon="mail" placeholder="E-mail" />
            <Input name="password" icon="lock" placeholder="Senha" />

            <Button>Entrar</Button>

            <ForgotPassword>
              <ForgotPasswordText>Esqueci minha senha</ForgotPasswordText>
            </ForgotPassword>
          </Container>
        </ScrollView>
      </KeyboardAvoidingView>
    {/* ... */}
    </>
)

// ...

// ...

```

- Utilizamos o `KeyboardAvoidingView` definindo o comportamento apenas para ios pois no android tem um comportamento diferente
- Utilizamos um ScrollView para permitir o usuário rolar caso haja mais campos e a tela seja um pequena
- Os `Text` precisam ter uma tag `View` por volta para funcionarem com `KeyboardAvoidingView`

---

## Unform

- Utilizamos essa lib para trabalhar com formulários

- Instalar dependencias:

```bash
yarn add @unform/core @unform/mobile
```

- Ajustamos o component `src/components/Input/index.tsx`:

```tsx
import React, { useRef, useEffect } from 'react';
import { TextInputProps } from 'react-native';
// unform
import { useField } from '@unform/core';

import { Container, TextInput, Icon } from './styles';

interface InputProps extends TextInputProps {
  name: string;
  icon: string;
}

interface InputValueReference {
  value: string;
}

const Input: React.FC<InputProps> = ({ name, icon, ...rest }) => {

  const inputElementRef = useRef<any>(null);
  // unform
  const { registerField, defaultValue = '', fieldName, error } = useField(name);
  const inputValueRef = useRef<InputValueReference>({ value: defaultValue });

  useEffect(() => {
    // unform
    registerField<string>({
      name: fieldName,
      ref: inputValueRef.current,
      path: 'value',
      setValue(ref: any, value) {
        inputValueRef.current.value = value;
        inputElementRef.current.setNativeProps({ text: value });
      },
      clearValue() {
        inputValueRef.current.value = '';
        inputElementRef.current.clear();
      },
    });
  }, [fieldName, registerField]);

  return (
    <Container>
      <Icon name={icon} size={20} color="#666360" />
      <TextInput
        keyboardAppearance="dark"
        placeholderTextColor="#666360"
        defaultValue={defaultValue}
        onChangeText={value => {
          inputValueRef.current.value = value;
        }}
        {...rest}
      />
    </Container>
  );
};

export default Input;

```

- E para utilizarmos tem um exemplo em `src/pages/SignIn`:

```tsx
// ...

import { Form } from '@unform/mobile';
import { FormHandles } from '@unform/core';

import Input from '~/components/Input';
// ...

const SignIn: React.FC = () => {
  const formRef = useRef<FormHandles>(null);

  const handleSubmit = useCallback(data => {
    console.log(data);
  }, []);

  return (
    <>
      <KeyboardAvoidingView
        style={{ flex: 1 }}
        behavior={Platform.OS === 'ios' ? 'padding' : undefined}
        enabled
      >
        <ScrollView
          keyboardShouldPersistTaps="handled"
          contentContainerStyle={{ flex: 1 }}
        >
          <Container>
            <Image source={logo} />
            <View>
              <Title>Faça seu logon</Title>
            </View>

            {/* unform */}
            <Form
              style={{ width: '100%' }}
              ref={formRef}
              onSubmit={handleSubmit}
            >
              <Input name="email" icon="mail" placeholder="E-mail" />
              <Input name="password" icon="lock" placeholder="Senha" />
              {/* unform submitForm */}
              <Button onPress={() => formRef.current?.submitForm()}>
                Entrar
              </Button>
            </Form>

            <ForgotPassword>
              <ForgotPasswordText>Esqueci minha senha</ForgotPasswordText>
            </ForgotPassword>
          </Container>
        </ScrollView>
      </KeyboardAvoidingView>

      <CreateAccountButton onPress={() => navigation.navigate('SignUp')}>
        <Icon name="log-in" size={20} color="#ff9000" />
        <CreateAccountButtonText>Criar uma conta</CreateAccountButtonText>
      </CreateAccountButton>
    </>
  );
};

export default SignIn;

```

## Usabilidade entre Inputs de texto

- Quando solicitamos e-mail do usuário algo que podemos utilizar algumas props para melhorar a experiência do usuário:

```tsx
<Input
  autoCorrect={false}
  autoCapitalize="none"
  keyboardType="email-address"
  name="email"
  icon="mail"
  placeholder="E-mail"
  returnKeyType="next"
/>
```

- Quando solicitamos senha podemos adicionar uma propriedade para esconder os caracteres de senha:


```tsx
<Input
  name="password"
  icon="lock"
  placeholder="Senha"
  secureTextEntry
  returnKeyType="send"
  onSubmitEditing={() => formRef.current?.submitForm()}
/>
```

- Mudar o enter do teclado `returnKeyType`, submeter form `onSubmitEditing`
- Para não sugerir uma senha podemos utilizar a prop: `textContentType="newPassword"`, uma opção para preencher o campo com o valor que recebe do sms é o `textContentType="oneTimeCode"`
---

### Focus

- Da forma que está desenvolvido o TextInput como um subcomponent utilizando o unform precisamos ajustar algumas coisas

- Para passar uma ref de um component para outro, temos a page `src/pages/SignIn/index.tsx`:

```tsx
import React, { useCallback, useRef } from 'react';
// ...
// ...
 const passwordInputRef = useRef<TextInput>(null);

<Input
  onSubmitEditing={() => passwordInputRef.current?.focus()}
/>

 <Input
    ref={passwordInputRef}
  />
```

- Porém a propriedade ref funciona de um jeito diferente no react, simplesmente não consigo passar a ref diretamente para um custom component, preciso realizar procedimentos mais avançados, no component `src/components/Input/index.tsx` temos:

```tsx
import React, {
  useRef,
  useEffect,
  useImperativeHandle,
  forwardRef,
} from 'react';

```

- Utilizamos o `useImperativeHandle` para passar uma informação do component filho para o component pai.

```tsx
// criamos uma interface para informar as props que queremos obter do nosso paramentro, no caso o ref
interface InputRef {
  focus(): void;
}


// Como precisamos do ref utilizamos o React.RefForwardingComponent o qual espera dois tipos:
// <O tipo da ref, Os demais tipos> - isso é invertido mas é assim mesmo
const Input: React.RefForwardingComponent<InputRef, InputProps> = (
  { name, icon, ...rest },
  ref
) => {
  // ...
  // function e/ou prop que queremos passar para o component pai
  useImperativeHandle(ref, () => ({
    // Aqui dentro posso injetar qualquer informação ou function do component filho para o componente pai.
    focus() {
      inputElementRef.current.focus();
    },
  }));
  // ...
};
```

- Quando trabalhamos com `ref` ou seja quando um elemento recebe a prop ref ele precisa do `forwardRef`:

**Importante se não, não conseguimos passar a ref e dará erro**
```tsx
export default forwardRef(Input);
```

---

## Validação

- Primeiro precisamos adicionar a lib:

```bash
yarn add yup
```

- Bem como o pacote de tipagens

```bash
yarn add @types/yup -D
```

- Um exemplo de como utilizar a validação está em `src/pages/SignIn`

```tsx
// ...
import * as Yup from 'yup';
// ...

const handleSubmit = useCallback(async (data: SignInFormData) => {
    try {
      formRef.current?.setErrors({});
      const schema = Yup.object().shape({
        email: Yup.string()
          .required('E-mail obrigatório')
          .email('Digite um e-mail válido'),
        password: Yup.string().required('Senha obrigatória'),
      });

      await schema.validate(data, { abortEarly: false });
      // await signIn({
      //   email: data.email,
      //   password: data.password,
      // });

      // history.push('/');
    } catch (err) {
      if (err instanceof Yup.ValidationError) {
        const erros = getValidatorErros(err);

        formRef.current?.setErrors(erros);

        return;
      }

      Alert.alert(
        'Erro na autenticação',
        'Ocorreu um erro ao realizar login, cheque as credenciais.'
      );
    }
  }, []);

// ...
```

---

## Realizar o Login

- Primeiro precisamos instalar o axios:

```bash
yarn add axios
```

- Criar o arquivo `src/services/api.ts`

- No arquivo `src/pages/SignUp` importamos a api.

---

## Autenticação


- Para persistir os dados podemos utilizar o `AsyncStorage`:

```bash
yarn add @react-native-community/async-storage
```

- Para ios, acessamos a pasta ios e executamos o comando:

```bash
pod install
```

- Para utilizar autenticação criamos um hook em `src/hooks/auth.tsx`

- Criamos também uma especie de provider `src/hooks/index.tsx`

- E adicionamos esse component em `src/App.tsx`

- Por fim adicionamos a chamada de autenticação em `src/pages/SignIn`

---

## Rotas privadas e não privadas

- Criar um arquivo chamado `src/routes/auth.routes.tsx` e adicionar as rotas não privadas
- Criar um arquivo chamado `src/routes/app.routes.tsx` e adicionar as rotas privadas
- Criar o arquivo `src/routes/index.tsx` o qual chamará essas rotas, conforme estado, se o usuário estiver logado mostra as privadas, do contrário as não privadas

- O único problema é que como é feito uma verificação disso no AsyncStorage e como isso é assincrono, irá aparecer um pequeno flash de uma rota para outra, devido a essa verificação, diferente do que acontece com a web.

- Para resolver isso iremos utilizar um load que iremos controlar em `src/hooks/auth.tsx`


---

### Utilizar Flatlist com styled components

- Um exemplo disso pode ser encontrado em `src/pages/Dashboard/index.tsx` e `src/pages/Dashboard/styles.tsx`:

```tsx
<ProviderList
        data={providers}
        keyExtractor={provider => provider.id}
        renderItem={({ item }) => <Text>{item.name}</Text>}
      />
```

```ts
import { FlatList } from 'react-native';

export const ProviderList = styled(FlatList as new () => FlatList<Provider>)``;
```


---

### Date Picker para react native

- Podemos utilizar essa lib: [DateTimePicker](https://github.com/react-native-datetimepicker/datetimepicker)

- Instalação:

```shell
yarn add @react-native-community/datetimepicker
```

- Para IOS utilizar adicionalmente acessar a pasta `ios` e executar o comando:

```shell
pod install
```

---

## Flipper debug com react native

- Uma ferramenta para debugar o código é o [Flipper](https://fbflipper.com)
- Só precisa baixar e utilizar!!!


---

## Obter imagem da galeria ou da camera

- Para utilizar esse recurso iremos utilizar a lib [react native image picker](https://github.com/react-native-image-picker/react-native-image-picker)

---

## Editar imagem

- Para realizar edição de imagens podemos utilizar o [Image Editor](https://github.com/callstack/react-native-image-editor)
