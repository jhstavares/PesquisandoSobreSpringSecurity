# PesquisandoSobreSpringSecurity

# PesquisaSpringSecurity

## O que � o Spring Security? ##
Spring Security � uma estrutura de autentica��o e controle de acesso.
� o um padr�o para proteger aplicativos baseados em Spring.

Spring Security � uma estrutura que se concentra em fornecer autentica��o e
autoriza��o para aplicativos Java.

AN�LISE PESSOAL:

Spring Security: � uma ferramente do SPRING  que serve para autenticar e controlar o acesso dos usu�rios nas p�ginas webs,
manipula��o da mesma ou, em determindo projetado. Onde s� ser� poss�vel alterar o projeto, caso confirme sua autentifica��o.

## Como implementar o Spring Security dentro da API? ##
Para habilitar o Spring Security em um projeto, � necess�rio, al�m  de criar depend�ncias, criar tamb�m a classe de configura��o.
� nessa classe que se define os protocolos de autentica��o, autoriza��o, prote��o e armazenamento.

DEPEND�NCIA:

	<dependency>
		<groupld>org.springframework.boot</groupld>
		<artifactld>spring-boot-starter-security</artifactld>
	</dependency>

EXEMPLO DE CONFIGURA��O:

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

AN�LISE PESSOAL:

S� � poss�vel usar o m�todo Security em um projeto, depois, que colocar suas depend�ncias e criar a classe de configura��es.
Para que o projeto esteja  realmente seguro.

## O que � JWT? ##

Um JWT � um padr�o para autentica��o e troca de informa��es definido pela RFC7519. Nele � poss�vel armazenar de forma segura e
compacta objetos JSON. Este token � um c�digo Base64 e pode ser assinado usando um segredo ou par de chaves privadas/p�blicas.

## ""O que � RFC 7519?
O JWT � um padr�o (RFC-7519) de mercado que define como transmitir e armazenar objetos JSON de forma compacta e segura
entre diferentes aplica��es. Os dados nele contidos podem ser validados a qualquer momento, pois o token � assinado digitalmente.

AN�LISE PESSOAL:
O usu�rio s� cosegueria acessar ou fazer altera��o, depois de algumas confirma��es, geradas pelo token.

## Como implementar o JWT? ##

No processo de autoriza��o do JWT, o front-end (o cliente primeiramente envia algumas credenciais para se autenticar
(nome de usu�rio e senha). O servidor (a aplica��o com Spring) em seguida, verifica essas credenciais.

AN�LISE PESSOAL: Como dito acima, seria uma forma de valida��o de dados.

## O que � criptografia? ##

A criptografia � um conjunto de t�cnicas pensadas para proteger uma informa��o de modo que apenas o emissor e receptor consigam
compreend�-la. � utilizada em comunica��es digitais, como na troca de mensagens ou em pagamentos online.

AN�LISE PESSOAL:
� uma chave de seguran�a para proteger uma informa��o.

## O que � BCryptPasswordEncoder? ##

O Bcrypt oferece uma maior seguran�a do que os outros algoritmos criptogr�ficos porque cont�m uma vari�vel que � proporcional
� quantidade de processamento necess�rio para criptografar a informa��o desejada, tornando-o resistente a ataques do tipo ?for�a-bruta?.

AN�LISE PESSOAL:
T�cnicas pensadas para proteger uma informa��o de forma mais segura. Pois o mesmo � do tipo alfo-num�rico.
EX: 123abc


## Qual a diferen�a entre autentica��o e autoriza��o de acesso? ##

# Autentifica��o
verifica a identidade digital do usu�rio, ou seja, processo de verifica��o de uma identidade. � quando o usu�rio prova de fato quem ele �.

EXEMPLO: Ao logar-se em qualquer sistema que necessite deste procedimento, o usu�rio est� passando por um processo de autentica��o.

# Autoriza��o
� o processo que ocorre ap�s ser validada a autentica��o. Diz respeito aos privil�gios que s�o concedidos a determinado usu�rio ao utilizar
uma aplica��o.

Serve para verificar se determinado usu�rio ter� a permiss�o para utilizar, executar recursos ou manipular determinadas a��es, que � de fundamental
import�ncia dentro de uma aplica��o.

EXEMPLO:
Ap�s realizar a autentica��o no sistema, o usu�rio do financeiro ter� acesso apenas aos m�dulos correspondentes � realiza��o de seu trabalho,
como contas a pagar, contas a receber.

J�  funcion�rio que trabalha, por exemplo, no setor de RH, n�o ter� acesso aos m�dulos do financeiro, ficando restrito apenas aos m�dulos
necess�rios para realiza��o do seu trabalho.

Como: cadastro de funcion�rios, hist�rico de sal�rios e benef�cios, cadastro de cargos, controle de exames m�dicos.
