# Styled Components

Styled Components, React tabanlı bir CSS-in-JS (CSS-in-JavaScript) kütüphanesidir. Bu yaklaşım, React bileşenlerini oluştururken stil tanımlamalarını JavaScript kodu içine entegre etmeyi amaçlar.

Styled Components kullanmanın bazı avantajları şunlar olabilir:

1. **İzole Stil**: Her bileşen kendi stilini içerir ve başka bileşenlerin stilleri ile karışmaz. Bu, uygulama genelinde stil çatışmalarını en aza indirir. Sadece yüklenen componentlerin stillerini çalıştırır.
2. **Dinamik Stiller**: JavaScript kodu içinde stil tanımlayarak, bileşenlerinizin durumuna, prop'larına veya diğer verilere göre dinamik olarak stil uygulayabilirsiniz.
3. **Kod Okunabilirliği**: Bileşenin stilini, bileşenin kendisiyle aynı dosyada tutarak kodunuzun daha okunabilir ve bakımı daha kolay hale gelmesini sağlayabilirsiniz.
4. **Component-Based Styling**: Stil tanımlamalarını bileşen seviyesinde yaparak, bileşenlerinizin yeniden kullanılabilirliğini ve modülerliğini artırabilirsiniz.
5. **Önişlemci Desteği**: Styled Components, Sass veya Less gibi önişlemci dilleri kullanma ihtiyacını ortadan kaldırır. Stil tanımlamalarını doğrudan JavaScript içinde yapabilirsiniz.

### Styled Component Oluşturmak

Styled Components, React'ta stilize edilmiş bileşenler oluşturmanıza olanak tanır. Örneğin, **`styled.button`** kullanarak, her çağrıldığında **`<button>`** oluşturan bir bileşen oluşturabilirsiniz. İçine stil metotları ekleyerek özelleştirilmiş bileşenler yaratırsınız. Bu yaklaşım, bileşenlerinizi daha düzenli ve kolay yönetilebilir hale getirir. `styled.div` olarak kullandığımızda component her çağrıldığında bize `<div>` html etiketi döndürecektir.

```jsx
import styled from 'styled-components';

const DeleteButtonStyled = styled.button`
	display: inline-block;
  padding: 4px 8px;
  border: 2px solid gray;
  background-color: red;
`;
export default function App() {
	return (
    <DeleteButtonStyled>Danger Button</DeleteButtonStyled>
  );
}

export default DeleteButton;
```

Output :

![Opera Anlık Görüntü_2023-08-25_000134_127.0.0.1.png](Styled%20Components%20d964672692194314b8c9ac5cf32bf896/Opera_Anlk_Grnt_2023-08-25_000134_127.0.0.1.png)

```jsx
import styled from 'styled-components';
import Logo from './logo.png';

const Image = styled.img`
	max-width: 120px;
`;

export default function App() {
	return (
      <Image src={Logo} />
    );
  }
}

// Image componenti img html etiketi oluşturacağı için direk src attribute 'sini 
// ekleyebiliriz.
```

### Props almak ve kullanmak

Styled componentlere props değerleri göndererek dinamik bir şekilde stillerde değişiklik yapabiliriz. Styled componentler girilen propslara otomatik olarak içeriden ulaşabilir şekilde tasarlanıştır. Aşağıdaki örnekte `Button` adında bir styled component oluşturduk ve `background-color` özelliğinde eğer `$danger` adında bir props var ise rengi `red` yok ise `white` olacağını belirttik ve ardından componenti oluşturup props olarak `$danger` gönderdik.

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: ${(props) => props?.$danger ? 'red' : 'white'};
`;

export default function App() {
	return (
    <Button $danger>Danger Button</Button>
  );
}
```

Props ‘un içeriğini farklı yöntemlerle de dışarıya çıkarabiliriz.

```jsx
const Button = styled.button`
  background-color: ${({ $danger }) => $danger ? 'red' : 'white'};
`;

const Button = styled.button`
  background-color: ${({ $danger : colorDanger }) => colorDanger  ? 'red' : 'white'};
`;
```

### ****Extending****

Bir styled component ‘in özelliklerini türeterek yeni bir styled component oluşturmaya yarar. Farklı bir component ‘de ki birçok stil özelliğinin aynısına ihtiyacınız var ise bunları kopyalayıp yeni bir styled component oluşturabiliriz.

```jsx
import styled from 'styled-components';

const Button = styled.button`
  display: flex;
	flex-direction: row;
	justify-content: center;
	color: red;
`;

const ExtendButton = styled(Button)`
	color: yellow;
`;

// ExtendButton adından yeni bir styled component oluşturduk ve Button adındaki styled
// componentin tüm özelliklerini almasını belirttik (extend). Artık ExtendButton tüm
// özellikleri alacak ve sadece color: yellow olarak değişecek.
```

### Selector ve Alt Class Stillendirme

Styled component ‘de Scss tarzında alt class ‘ları stillendirebilir veya hover, active, focus vb. özellikleri kullanabiliriz.

```jsx
import styled from 'styled-components';

const Container = styled.div`
  display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;

	.title {
		font-size: 24px;
		font-weight: bold;
		color: red;

		&:hover {
			color: blue;
		}
	}
`;

export default function App() {
	return (
    <Container>
				<h1 className="title">Hellow Styled Components</h1>
		</Container>
  );
}

// Container div 'inin altında bulunan title class 'ına ait html etiktinini stillendirdik.
```

### HTML Tag Attributes

Oluşturduğumuz html etiketlerine styled componentlerimizden yeni `attribute` ‘lar ekleyebilir veya düzenleyebiliriz. `attrs` bir obje alır ve içerisinde `attribute` ‘larımızı tanımlayabiliriz.

```jsx
import styled from 'styled-components';

const Button = styled.button.attrs({type:'submit'})`
  display: flex;
	flex-direction: row;
	justify-content: center;
	color: red;
`;

export default function App() {
	return (
    <Button>Gönder</Button >
  );
}

// button html etiketinin tipi artık submit olacaktır.
```

```jsx
import styled from 'styled-components';

const Link = styled.a.attrs({href:'https://github.com/burakkrt', target:'_blank'})`
	color: blue;
  cursor: pointer;
  text-decoration: underline;
`;

export default function App() {
	return (
    <Link>Beni takip et</Link >
  );
}

// Link componentine href ve target attribute 'lerini ekledik.
```

### HTML Tag Props Almak

Stil işlemelerinde propslara erişebildiğimiz gibi attrs işlemleride bize otomatik props değerlerini gönderir. Bu isteğe bağlıdır kullanılabilir.

```jsx
import styled from 'styled-components';

const Link = styled.a.attrs((porps) => 
({href:props?.link || 'https://github.com/burakkrt', target:'_blank'}))`
	color: blue;
  cursor: pointer;
  text-decoration: underline;
`;

export default function App() {
	return (
    <Link link="https://www.linkedin.com/in/kurt-burak/">Beni takip et</Link >
  );
}

// Link componentine link adında bir props gönderdiğimizde href etiketi artık bu
// değeri alacak, eğer link adında props göndermek isek github linkini ekleyecek.
```

### Keyframes ve Animate

```jsx
import styled, {keyframes} from 'styled-components';

const rotate = keyframes`
	from {
		transfrom: rotate(0deg);
	}
	to {
		transform: rotate(360deg);
	}
`;

const Kutu = styled.div`
	width: 50px;
	height: 50px;
	background-color: red;
	border-radius: 15px
	position: relative;
	animaion: ${rotate} 5s linear infinite;
`;

export default function App() {
	return (
    <Kutu/>
  );
}

```

### ThemeProvider

Tüm bileşenlerimizi sarmalayan ThemeProvider componenti ile alt bileşenlerde erişebileceğimiz theme props ‘u oluşturabilir ve bu props ‘un özelliklerine göre stillerimizi dinamik hale getirebiliriz.

`<ThemeProvider>` ‘ı kullanmak için en üst componentte tüm componentleri sarmalayacak şekilde tanımlarız ve içerisine `theme` olarak obje türünde bir `props` alır. Arından alt bileşenlerde `props.theme` olarak çağırıp kullanabiliriz.

```jsx
import styled, {ThemeProvider} from 'styled-components';

// props olarak gönderdiğimiz theme nın içerisinden dark.background 'u alıyoruz.
export const CustomButton = styled`
  background-color: ${(props) => props.theme.dark.background};
`;

// Provider 'a props olarak gönderilecek objeyi tanımlıyoruz.
const theme = {
  dark: {
    background: "#121212",
    text: "#fff"
  },
  light: {
    background: "#fff",
    text: "#121212"
  }
};

// en üst bileşende alt componentleri sarmalayarak theme props 'unu gönderiyoruz.
function App() {
	return (
    <>
			<ThemeProvider theme={theme}>
	      <CustomButton>Test</CustomButton>
			</ThemeProvider>
    </>
  )
}
```

### GlobalStyle

Stil componentleri ilgili component yüklendiği zaman çalışan birbirinden bağımsız bileşenlerdir. Buda diğer stil sınıfları ile çakışmasını önlerken tüm ihtiyac olunan stillerin yüklenmesini sağlayarak performansı arttır. Componentlere özel stil bileşenlerinden farklı olarak tüm proje genelinde kullanımasını istediğimiz stilleri createGlobalStyle componenti ile tanımlarız.

```jsx
import {createGlobalStyle} from 'styled-components';
// Aşağıdaki örnekte bir önceki konudaki themeprovider lar tanımlanmış varsayılır.

// createGlobalStyle bileşeninden yeni bir GlobalStyled componenti oluşturduk.
const GlobalStyle = createGlobalStyle`
	*{
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	body {
		background-color: ${(props) => props.theme.dark.background}
	}
`;

// GlobalStyle 'yi en üst bileşende themeProvider 'ın altında çağırığ çalıştırdık. 
// Farklı yerlerde de kullanabilabilir ama en iyi verim almak için burada çağırdık.
function App() {
	return (
    <>
			<ThemeProvider theme={theme}>
				<GlobalStyle/>
	      <CustomButton>Test</CustomButton>
			</ThemeProvider>
    </>
  )
}
```