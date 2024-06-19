*** Settings ***
Documentation        Suite de testes de cadastro de dog walker 

Resource    ../resources/base.resource


*** Test Cases ***
Deve poder cadastrar um novo dog walker
     ${dog_walker}    Create Dictionary    
    ...    nome=Calila QA
    ...    email=CalilaQA@tester.com
    ...    cpf=02986097030
    ...    cep=04534011
    ...    street=Rua Joaquim Floriano
    ...    district=Itaim Bibi
    ...    city_uf=São Paulo/SP
    ...    number=1000
    ...    details=Apto 28
    ...    cnh=toretto.jpg

#Encapisulamento 
    Start session
    Go to signup page
    Fill signup form    ${dog_walker} 
    Submit signup form
    Popup should be    Recebemos o seu cadastro e em breve retornaremos o contato.  
    Finish session

Não deve cadastrar se os campos obrigatorios não forem preenchido 
    [Tags]    required
    
    # ${dog_walker}    Create Dictionary    
    #...    nome=Calila QA
    #...    email=CalilaQA@tester.com
    #...    cpf=02986097030
    #...    cep=04534011
    #...    street=Rua Joaquim Floriano
    #...    district=Itaim Bibi
    #...    city_uf=São Paulo/SP
    #...    number=1000
    #...    details=Apto 28
    #...    cnh=toretto.jpg

#Encapisulamento 
    Start session
    Go to signup page
    #Fill signup form    ${dog_walker} 
    Submit signup form
    #Popup should be    Recebemos o seu cadastro e em breve retornaremos o contato.  
    Finish session


Não deve cadastrar se os campos obrigatórios não forem preenchidos required
    [Tags]    required

    Start session
    Go to signup page
    Submit signup form

    Alert should be    Informe o seu nome completo
    Alert should be    Informe o seu melhor email
    Alert should be    Informe o seu CPF
    Alert should be    Informe o seu CEP
    Alert should be    Informe um número maior que zero
    Alert should be    Adcione um documento com foto (RG ou CHN)

    Finish session

Não deve cadastrar se o cpf for incorreto    
    [Tags]    cpf_inv

    ${dog_walker}    Create Dictionary    
    ...    nome=Calila QA
    ...    email=CalilaQA@tester.com
    ...    cpf=02986097Aaa
    ...    cep=04534011
    ...    street=Rua Joaquim Floriano
    ...    district=Itaim Bibi
    ...    city_uf=São Paulo/SP
    ...    number=1000
    ...    details=Apto 28
    ...    cnh=toretto.jpg

#Encapisulamento 
    Start session
    Go to signup page
    Fill signup form    ${dog_walker} 
    Submit signup form  
    #Alert should be     CPF inválido  
    Finish session
    
    


