# PesquisandoSobreSpringSecurity

# PesquisaSpringSecurity

## O que é o Spring Security? ##
Spring Security é uma estrutura de autenticação e controle de acesso.
É o um padrão para proteger aplicativos baseados em Spring.

Spring Security é uma estrutura que se concentra em fornecer autenticação e
autorização para aplicativos Java.

ANÁLISE PESSOAL:

Spring Security: É uma ferramente do SPRING  que serve para autenticar e controlar o acesso dos usuários nas páginas webs,
manipulação da mesma ou, em determindo projetado. Onde só será possível alterar o projeto, caso confirme sua autentificação.

## Como implementar o Spring Security dentro da API? ##
Para habilitar o Spring Security em um projeto, é necessário, além  de criar dependências, criar também a classe de configuração.
É nessa classe que se define os protocolos de autenticação, autorização, proteção e armazenamento.

DEPENDÊNCIA:

	<dependency>
		<groupld>org.springframework.boot</groupld>
		<artifactld>spring-boot-starter-security</artifactld>
	</dependency>

EXEMPLO DE CONFIGURAÇÃO:

@Configuration
@EnableConfigurationProperties

public class SecurityConfig extends WebSecurityConfigurerAdapter {

@Autowired
private MyUserDetailsService userDetailsService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
		.httpBasic()
                .and()
                .authorizeRequests()
                .antMatchers("/h2-console/**").permitAll()
                .antMatchers("/").permitAll()
                .antMatchers("/books").hasRole("USER")
                .antMatchers("/books2").hasRole("ADMIN")
                .and()
                .csrf().disable()
                .headers().frameOptions().disable();
    }
	
    @Override
    protected void configure(AuthenticationManagerBuilder builder) throws Exception {
        builder
                .userDetailsService(userDetailsService)
                .passwordEncoder(new BCryptPasswordEncoder());
    }

}

ANÁLISE PESSOAL:

Só é possível usar o método Security em um projeto, depois, que colocar suas dependências e criar a classe de configurações.
Para que o projeto esteja  realmente seguro.

## O que é JWT? ##

Um JWT é um padrão para autenticação e troca de informações definido pela RFC7519. Nele é possível armazenar de forma segura e
compacta objetos JSON. Este token é um código Base64 e pode ser assinado usando um segredo ou par de chaves privadas/públicas.

## ""O que é RFC 7519?
O JWT é um padrão (RFC-7519) de mercado que define como transmitir e armazenar objetos JSON de forma compacta e segura
entre diferentes aplicações. Os dados nele contidos podem ser validados a qualquer momento, pois o token é assinado digitalmente.

ANÁLISE PESSOAL:
O usuário só cosegueria acessar ou fazer alteração, depois de algumas confirmações, geradas pelo token.

## Como implementar o JWT? ##

No processo de autorização do JWT, o front-end (o cliente primeiramente envia algumas credenciais para se autenticar
(nome de usuário e senha). O servidor (a aplicação com Spring) em seguida, verifica essas credenciais.

ANÁLISE PESSOAL: Como dito acima, seria uma forma de validação de dados.

## O que é criptografia? ##

A criptografia é um conjunto de técnicas pensadas para proteger uma informação de modo que apenas o emissor e receptor consigam
compreendê-la. É utilizada em comunicações digitais, como na troca de mensagens ou em pagamentos online.

ANÁLISE PESSOAL:
É uma chave de segurança para proteger uma informação.

## O que é BCryptPasswordEncoder? ##

O Bcrypt oferece uma maior segurança do que os outros algoritmos criptográficos porque contém uma variável que é proporcional
à quantidade de processamento necessário para criptografar a informação desejada, tornando-o resistente a ataques do tipo ?força-bruta?.

ANÁLISE PESSOAL:
Técnicas pensadas para proteger uma informação de forma mais segura. Pois o mesmo é do tipo alfo-numérico.
EX: 123abc


## Qual a diferença entre autenticação e autorização de acesso? ##

# Autentificação
verifica a identidade digital do usuário, ou seja, processo de verificação de uma identidade. É quando o usuário prova de fato quem ele é.

EXEMPLO: Ao logar-se em qualquer sistema que necessite deste procedimento, o usuário está passando por um processo de autenticação.

# Autorização
é o processo que ocorre após ser validada a autenticação. Diz respeito aos privilégios que são concedidos a determinado usuário ao utilizar
uma aplicação.

Serve para verificar se determinado usuário terá a permissão para utilizar, executar recursos ou manipular determinadas ações, que é de fundamental
importância dentro de uma aplicação.

EXEMPLO:
Após realizar a autenticação no sistema, o usuário do financeiro terá acesso apenas aos módulos correspondentes à realização de seu trabalho,
como contas a pagar, contas a receber.

Já  funcionário que trabalha, por exemplo, no setor de RH, não terá acesso aos módulos do financeiro, ficando restrito apenas aos módulos
necessários para realização do seu trabalho.

Como: cadastro de funcionários, histórico de salários e benefícios, cadastro de cargos, controle de exames médicos.
