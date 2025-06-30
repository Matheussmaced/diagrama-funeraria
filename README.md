```mermaid
classDiagram
    %% Componentes React
    class App {
        - user
        - userId
        - currentPage
        + handleLogout()
        + addGame()
        + setPage
    }

    class LandingPage

    class Auth {
        + handleLogin()
        + handleSignup()
    }

    class Dashboard {
        - selectedGameId
        + updateGameStatus()
        + uploadImage()
    }

    class GameDetail {
        - gameId
        + completeAchievement()
        + updateGameProgress()
    }

    class UserSearch {
        - selectedUserIdToDisplay
        + performSearch()
    }

    class PublicProfile {
        - userId
        + displayGames()
    }

    class ImageGallery

    %% Firebase Services
    class FirebaseApp
    class FirestoreDB
    class FirebaseAuth
    class FirebaseStorage

    %% Data Models
    class Jogo {
        id
        title
        platform
        status
        imageUrl
    }

    class Conquista {
        id
        description
        completed
    }

    class JogoPublico {
        gameId
        ownerId
        title
        platform
        status
        imageUrl
    }

    %% Relações
    App --> LandingPage : renderiza
    App --> Auth : renderiza
    App --> Dashboard : renderiza
    App --> UserSearch : renderiza
    App --> PublicProfile : renderiza
    App --> ImageGallery : renderiza

    Auth ..> FirebaseAuth : usa

    Dashboard ..> FirestoreDB : lê/escreve jogos
    Dashboard ..> FirebaseStorage : upload imagens
    Dashboard --> GameDetail : passa selectedGameId

    GameDetail ..> FirestoreDB : lê/escreve conquistas
    GameDetail ..> FirebaseStorage : obtém imagem

    UserSearch ..> FirestoreDB : busca public_games
    UserSearch --> PublicProfile : passa selectedUserIdToDisplay

    PublicProfile ..> FirestoreDB : lê public_games

    %% Fluxos de dados
    Dashboard --> Jogo : manipula
    GameDetail --> Conquista : manipula
    PublicProfile --> JogoPublico : manipula

    %% Firebase App
    App ..> FirebaseApp : inicializa

