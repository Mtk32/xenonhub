repita task.wait() até que game:IsLoaded()
start_script_time = tick()
repita task.wait() até que game:GetService("Players").LocalPlayer
repita task.wait()
    pcall(function()
        para i, v em pares(getconnections(game.Players.LocalPlayer.PlayerGui["Main (minimal)"].ChooseTeam.Container[(getgenv().Team or "Pirates")].Frame.TextButton.Activated)) faça
            v.Função()
        fim
    fim)
até que game:GetService("Players").LocalPlayer.Team ~= nil
local plr = game:GetService("Players").LocalPlayer
local WS, RunService, ReplicatedStorage, Lighting, Players = workspace, game:GetService("RunService"), game:GetService("ReplicatedStorage"), game:GetService("Lighting"), game:GetService("Players")
local Calisucvat = {}
local VirtualInputManager = game:GetService("VirtualInputManager")
local RenderStepped, Stepped = RunService.Stepped, RunService.RenderStepped
local CommF_ = ReplicatedStorage.Remotes:WaitForChild("CommF_")
local Modules = ReplicatedStorage:WaitForChild("Modules")
local Net = Modules:WaitForChild("Net")
local Quests = require(ReplicatedStorage:WaitForChild("Quests"))
local GuideModule = require(ReplicatedStorage:WaitForChild("GuideModule"))
local Register_Attack, Register_Hit = Net:WaitForChild("RE/RegisterAttack"), Net:WaitForChild("RE/RegisterHit")
instância local = {obj = {}}
objeto local = instância.obj
local HttpService = game:GetService("HttpService")
LoadedHub local
local Validator = game.ReplicatedStorage.Remotes:WaitForChild("Validator2")
local ShootRemote = game.ReplicatedStorage.Modules.Net:WaitForChild("RE/ShootGunEvent")
local CurrentExecutor = identifyexecutor()
local LeviathanHuntPos = Vector3.new(-99999999.21484375, 37.18704697489738464, 656.7513427734375).Unit
local FastAttack = {}
local FastAttack_enemies = workspace:WaitForChild("Enemies")
local FastAttack_characters = workspace:WaitForChild("Characters")
local FastAttack_arms = { "BraçoInferiorDireito", "BraçoSuperiorDireito", "BraçoInferiorEsquerdo", "BraçoSuperiorEsquerdo", "MãoDireita", "MãoEsquerda" }
local FastAttack_sendHits
local FastAttack_combatThread
pcall(function()
    FastAttack_combatThread = require(ReplicatedStorage:WaitForChild("Modules"):WaitForChild("Flags")).COMBAT_REMOTE_THREAD ou false
fim)
função local FastAttack_GetSendHits()
    Se não getsenv, retorne nil.
    local playerScripts = plr:FindFirstChild("PlayerScripts")
    Se não houver scripts de jogador, retorne nulo.
    para _, s em ipairs(playerScripts:GetChildren()) faça
        Se s:IsA("LocalScript") então
            local ok, env = pcall(getsenv, s)
            se ok e env e env._G e env._G.SendHitsToServer então
                return env._G.SendHitsToServer
            fim
        fim
    fim
    retornar nulo
fim
função local FastAttack_EnsureSendHits()
    se getsenv e FastAttack_sendHits == nil então
        FastAttack_sendHits = FastAttack_GetSendHits()
    fim
fim
função AtaqueRápido:SuperAtaqueRápido()
    caractere local = plr.Character
    Se não for um caractere, retorne o fim.
    local hum = char:FindFirstChild("Humanoid")
    Se não hum ou hum.Saúde <= 0, então retorne fim.
    raiz local = char:FindFirstChild("HumanoidRootPart")
    Se não for raiz, retorne fim.
    ferramenta local
    para _, c em ipairs(char:GetChildren()) faça
        Se c:IsA("Tool") então
            ferramenta = c
            quebrar
        fim
    fim
    Se não for a ferramenta, retorne ao fim.
    local hitData = {}
    Parte primária local
    para _, lista em ipairs({ FastAttack_enemies, FastAttack_characters }) faça
        Se for uma lista, então
            para _, e em lista:GetChildren() faça
                se e ~= char e não e:GetAttribute("IsBoat") então
                    local ehum = e:FindFirstChild("Humanóide")
                    local ebody = e:FindFirstChild("Head") ou e.PrimaryPart
                    se ehum e ehum.Saúde > 0 e ebody e (ebody.Posição - root.Posição).Magnitude <= 80 então
                        parte local = e:FindFirstChild(FastAttack_arms[math.random(#FastAttack_arms)]) ou e.PrimaryPart
                        se parte então
                            tabela.inserir(hitData, { e, parte })
                            PartePrimária = parte
                        fim
                    fim
                fim
            fim
        fim
    fim
    se #hitData == 0 ou não primaryPart então retorne fim
    local lcr = tool:FindFirstChild("LeftClickRemote")
    se lcr então
        pcall(function()
            lcr:FireServer((primaryPart.Position - root.Position).Unit, 1)
        fim)
    fim
    Register_Attack:FireServer(0)
    Se FastAttack_combatThread então
        FastAttack_EnsureSendHits()
        Se FastAttack_sendHits então
            FastAttack_sendHits(primaryPart, hitData)
        outro
            Register_Hit:FireServer(primaryPart, hitData)
        fim
    outro
        Register_Hit:FireServer(primaryPart, hitData)
    fim
fim
Hub = {}
Hub.Title = "Dwac Hub" .. (getgenv().Premium and " [Premium]" or getgenv().Developer and " [Developer]" or " [Beta]")
Hub.Game = "BloxFruits"

local Fluent = loadstring(game:HttpGet("https://raw.githubusercontent.com/huyyeuemhihi/Fluent/refs/heads/main/Fluentvip.lua"))()

local Window = Fluent:CreateWindow({
    Título = Hub.Title,
    Subtítulo = "por @it_kuridev e @dzvaiooo",
    TabWidth = 160,
    Tamanho = UDim2.fromOffset(580, 460),
    Acrílico = falso,
    Tema = "Escuro",
    MinimizeKey = Enum.KeyCode.LeftControl
})

Opções locais = Fluent.Options

Notificar = função(título, conteúdo, duração)
    Fluent:Notify({
        Título = título ou "Dwac Hub",
        Conteúdo = conteúdo ou "...",
        Duração = duração ou 5
    })
fim

se CurrnetExecutor == "Wave" ou CurrnetExecutor == "AWP" ou CurrnetExecutor == "Posstasium" então
    Notify("Dwac Hub","Seu executor atual suporta todas as funções, algumas funções funcionarão bem", 3)
outro
    Notify("Dwac Hub","Seu executor atual não suporta todas as funções, algumas funções não funcionarão", 3)
fim

plr.Idled:Connect(function()
    game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    task.wait(1)
    game:GetService("VirtualUser"):Button1Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
fim)

local RandomText = {
    [1] = "Bem-vindo ao meu script",
    [2] = "Seu pai gordo",
    [3] = "Sua mãe gorda",
    [4] = "?",
    [5] = "Oh olá homens gordos",
    [6] = "Você está banido",
    [7] = "sua gordura"
}

módulo local, Configurações = {}, {
    ["Ataque Rápido"] = verdadeiro,
    ["Distância de Trazer"] = 350,
    ["Velocidade intermediária"] = 300,
    ["Auto Buso"] = verdadeiro,
}

module.Mobs = {
    CakeMobs = {
        "Cookie Crafter",
        "Protetor de Bolo",
        "Equipe de Confeitaria",
        "Padeiro Chefe"
    },
    BoneMobs = {
        "Esqueleto Renascido",
        "Zumbi Vivo",
        "Alma Demoníaca",
        "Múmia Possuída"
    },
    EliteMobs = {
        "Urbano",
        "Deandre",
        "Diablo"
    },
    TikiMobs = {
        "Garoto da Ilha",
        "Fora da Lei da Ilha",
        "Campeão da Ilha",
        "Caçador de Serpentes",
        "Matador de Crânios",
        "Guerreiro Beijado pelo Sol"
    },
    RengokuMobs = {
        "Guerreiro do Ártico",
        "Espreitador da Neve"
    },
    ripindra = {
        "rip_indra",
        "rip_indra True Form"
    },
    CocoaMobs = {
        "Guerreiro do Cacau",
        "Batalha de Barras de Chocolate",
        "Candy Rebel",
        "Doce Ladrão",
    },
    SeaMobs = {
        "Tubarão",
        "Membro da Tripulação de Pesca",
        "Piranha",
        "Terrorshark"
    }
}

module.Berries = {
    "Amora Azul Gelo",
    "Green Toad Berry",
    "Laranja e Frutas Vermelhas",
    "Pink Pig Berry"
}

module.Bosses = {
    ["Especialista em Sabres"] = {
        NoQuest = true,
        Posição = CFrame.new(-1461, 30, -51)
    },
    ["A Serra"] = {
        RaidBoss = true,
        Posição = CFrame.new(-690, 15, 1583)
    },
    ["Greybeard"] = {
        RaidBoss = true,
        Posição = CFrame.new(-5043, 25, 4262)
    },
    ["O Rei Gorila"] = {
        IsBoss = true,
        Nível = 20,
        Posição = CFrame.new(-1128, 6, -451),
        Missão = {"JungleQuest", CFrame.new(-1598, 37, 153)}
    },
    ["Chef"] = {
        IsBoss = true,
        Nível = 55,
        Posição = CFrame.new(-1131, 14, 4080),
        Missão = {"BuggyQuest1", CFrame.new(-1140, 4, 3829)}
    },
    ["Yeti"] = {
        IsBoss = true,
        Nível = 105,
        Posição = CFrame.new(1185, 106, -1518),
        Missão = {"SnowQuest", CFrame.new(1385, 87, -1298)}
    },
    ["Vice-Almirante"] = {
        IsBoss = true,
        Nível = 130,
        Posição = CFrame.new(-4807, 21, 4360),
        Quest = {"MarineQuest2", CFrame.new(-5035, 29, 4326), 2}
    },
    ["Cisne"] = {
        IsBoss = true,
        Nível = 240,
        Posição = CFrame.new(5230, 4, 749),
        Quest = {"ImpelQuest", CFrame.new(5191, 4, 692)}
    },
    ["Chefe de Guarda"] = {
        IsBoss = true,
        Nível = 230,
        Posição = CFrame.new(5230, 4, 749),
        Quest = {"ImpelQuest", CFrame.new(5191, 4, 692), 2}
    },
    ["Guardião"] = {
        IsBoss = true,
        Nível = 220,
        Posição = CFrame.new(5230, 4, 749),
        Quest = {"ImpelQuest", CFrame.new(5191, 4, 692), 1}
    },
    ["Almirante Magma"] = {
        IsBoss = true,
        Nível = 350,
        Posição = CFrame.new(-5694, 18, 8735),
        Missão = {"MagmaQuest", CFrame.new(-5319, 12, 8515)}
    },
    ["Senhor Homem-Peixe"] = {
        IsBoss = true,
        Nível = 425,
        Posição = CFrame.new(61350, 31, 1095),
        Quest = {"FishmanQuest", CFrame.new(61122, 18, 1567)}
    },
    ["Wysper"] = {
        IsBoss = true,
        Nível = 500,
        Posição = CFrame.new(-7927, 5551, -637),
        Missão = {"SkyExp1Quest", CFrame.new(-7861, 5545, -381)}
    },
    ["Deus do Trovão"] = {
        IsBoss = true,
        Nível = 575,
        Posição = CFrame.new(-7751, 5607, -2315),
        Missão = {"SkyExp2Quest", CFrame.new(-7903, 5636, -1412)}
    },
    ["Cyborg"] = {
        IsBoss = true,
        Nível = 675,
        Posição = CFrame.new(6138, 10, 3939),
        Quest = {"FountainQuest", CFrame.new(5258, 39, 4052)}
    },
    ["Don Swan"] = {
        RaidBoss = true,
        Posição = CFrame.new(2289, 15, 808)
    },
    ["Capitão Amaldiçoado"] = {
        RaidBoss = true,
        Posição = CFrame.new(912, 186, 33591)
    },
    ["Darkbeard"] = {
        RaidBoss = true,
        Posição = CFrame.new(3695, 13, -3599)
    },
    ["Diamante"] = {
        IsBoss = true,
        Nível = 750,
        Posição = CFrame.new(-1569, 199, -31),
        Missão = {"Area1Quest", CFrame.new(-427, 73, 1835)}
    },
    ["Jeremy"] = {
        IsBoss = true,
        Nível = 850,
        Posição = CFrame.new(2316, 449, 787),
        Missão = {"Area2Quest", CFrame.new(635, 73, 919)}
    },
    ["Orbitus"] = {
        IsBoss = true,
        Nível = 925,
        Posição = CFrame.new(-2086, 73, -4208),
        Missão = {"MarineQuest3", CFrame.new(-2441, 73, -3219)}
    },
    ["Almirante da Fumaça"] = {
        IsBoss = true,
        Nível = 1150,
        Posição = CFrame.new(-5078, 24, -5352),
        Missão = {"IceSideQuest", CFrame.new(-6061, 16, -4904)}
    },
    ["Almirante de Gelo Desperto"] = {
        IsBoss = true,
        Nível = 1400,
        Posição = CFrame.new(6473, 297, -6944),
        Missão = {"FrostQuest", CFrame.new(5668, 28, -6484)}
    },
    ["Guardião das Marés"] = {
        IsBoss = true,
        Nível = 1475,
        Posição = CFrame.new(-3711, 77, -11469),
        Missão = {"ForgottenQuest", CFrame.new(-3056, 240, -10145)}
    },
    ["Tirano dos Céus"] = {
        RaidBoss = true,
        Posição = CFrame.new(-16252, 153, 1394)
    },
    ["Príncipe do Bolo"] = {
        RaidBoss = true,
        Posição = CFrame.new(-2103, 70, -12165)
    },
    ["Rei da Massa"] = {
        RaidBoss = true,
        Posição = CFrame.new(-2103, 70, -12165)
    },
    ["rip_indra Forma Verdadeira"] = {
        RaidBoss = true,
        Posição = CFrame.new(-5333, 424, -2673)
    },
    ["Pedra"] = {
        IsBoss = true,
        Nível = 1550,
        Posição = CFrame.new(-1049, 40, 6791),
        Quest = {"PiratePortQuest", CFrame.new(-449, 109, 5950)}
    },
    ["Líder da Hydra"] = {
        IsBoss = true,
        Nível = 1675,
        Posição = CFrame.new(5836, 1019, -83),
        Missão = {"VenomCrewQuest", CFrame.new(5214, 1004, 761)}
    },
    ["Kilo Admiral"] = {
        IsBoss = true,
        Nível = 1750,
        Posição = CFrame.new(2904, 509, -7349),
        Quest = {"MarineTreeIsland", CFrame.new(2485, 74, -6788)}
    },
    ["Capitão Elefante"] = {
        IsBoss = true,
        Nível = 1875,
        Posição = CFrame.new(-13393, 319, -8423),
        Missão = {"DeepForestIsland", CFrame.new(-13233, 332, -7626)}
    },
    ["Bela Pirata"] = {
        IsBoss = true,
        Nível = 1950,
        Posição = CFrame.new(5370, 22, -89),
        Missão = {"DeepForestIsland2", CFrame.new(-12682, 391, -9901)}
    },
    ["Rainha dos Bolos"] = {
        IsBoss = true,
        Nível = 2175,
        Posição = CFrame.new(-710, 382, ​​-11150),
        Missão = {"IceCreamIslandQuest", CFrame.new(-818, 66, -10964)}
    },
    ["Longma"] = {
        NoQuest = true,
        Posição = CFrame.new(-10218, 333, -9444)
    }
}

module.Getboss = function(Boss)
    para r,v no próximo módulo.Chefes fazem
        se r == Boss e v.IsBoss então
            retornar r,v
        fim
    fim
fim

NPCs = {}
para _,v em próximo, ReplicatedStorage.NPCs:GetChildren() faça
    tabela.inserir(NPCs, v)
fim
para _,v em próximo, WS.NPCs:GetChildren() faça
    tabela.inserir(NPCs, v)
fim

print(RandomText[math.random(1, #RandomText)])

módulo.novo = função(nome, configuração)
    local gaya = Instance.new(name)
    para índice, valor em próximo, configuração faça
        gaya[index] = valor
    fim
    retornar gaya
fim

module.Save = function()
    se não isfolder("Dwac Hub") então
        makefolder("Dwac Hub")
    fim
    se não isfolder("Dwac Hub/Settings") então
        makefolder("Dwac Hub/Configurações")
    fim
    writefile("Dwac Hub/Settings/" .. Hub.Game .. "-" .. plr.Name .. ".json", HttpService:JSONEncode(Settings))
fim

module.Read = function()
    p1, p2 = pcall(function()
        se não isfolder("Dwac Hub") então
            module.Save()
        fim
        return HttpService:JSONDecode(readfile("Dwac Hub/Settings/" .. Hub.Game .. "-" .. plr.Name .. ".json"))
    fim)
    se p1 então
        retornar p2
    outro
        module.Save()
        return module.Read()
    fim
fim

Configurações = módulo.Read()

local ShopTab = Window:AddTab({ Title = "Aba Loja", Icon = "rbxassetid://134556077676632" })
ShopTab:AddSection("Itens em Rolamento")
ShopTab:AddButton({
    Título = "Resgatar todos os códigos"
    Callback = função()
        Códigos locais = {
            "BANEXPLOIT", "NOMOREHACK", "WildDares", "BossBuild", "GetPranked",
            "GANHE_FRUTAS", "SUB2GAMERROBOT_RESET1", "KITT_RESET", "GrandesNotícias", "CHANDLER",
            "Fudd10", "fudd10_v2", "Sub2UncleKizaru", "FIGHT4FRUIT", "kittgaming",
            "TRIPLEABUSE", "Sub2CaptainMaui", "Sub2Fer999", "Enyu_is_Pro", "Magicbus",
            "JCWK", "Starcodeheo", "Bluxxy", "SUB2GAMERROBOT_EXP1", "Sub2NoobMaster123",
            "Sub2Daigrock", "Axiore", "TantaiGaming", "StrawHatMaine", "Sub2OfficialNoobie",
            "TheGreatAce", "JULYUPDATE_RESET", "ADMINHACKED", "SEATROLLING", "24NOADMIN",
            "ADMIN_TROLL", "NEWTROLL", "SECRET_ADMIN", "batalha de pessoal", "NOEXPLOIT",
            "NOOB2ADMIN", "CODESLIDE", "fruitconcepts", "krazydares"
        }
        para _, v em seguida, Códigos fazem
            ReplicatedStorage.Remotes.Redeem:InvokeServer(v)
        fim
    fim
})
local RandomSuprises = ShopTab:AddToggle("Surpresas Aleatórias", {
    Título = "Surpresas Aleatórias"
    Descrição = "Rolar ossos automaticamente",
    Padrão = Configurações["Surpresas Aleatórias"] ou falso,
    Callback = function(v)
        Configurações["Surpresas Aleatórias"] = v
        module.Save()
    fim
})

ShopTab:AddSection("Estilo de Luta")
local SelectMelee = ShopTab:AddDropdown("Selecionar Melee", {
    Título = "Selecionar Combate Corpo a Corpo",
    Descrição = "Selecione qualquer arma corpo a corpo que você queira comprar",
    Valores = {"Pernas Negras", "Elétrico", "Caratê Homem-Peixe", "Garra de Dragão", "Super-humano", "Passo da Morte", "Garra Elétrica", "Caratê Homem-Tubarão", "Garra de Dragão", "Deus-humano", "Arte Sanguínea"}
    Padrão = "",
    Callback = function(v)
        se v == "Pernas Pretas" então
            module.FireRemotes("BuyBlackLeg")
        senão se v == "Eletro" então
            module.FireRemotes("BuyElectro")
        senão se v == "Caratê Homem-Peixe" então
            module.FireRemotes("BuyFishmanKarate")
        senão se v == "Garra de Dragão" então
            module.FireRemotes("BlackbeardReward", "DragonClaw", "1")
            module.FireRemotes("BlackbeardReward", "DragonClaw", "2")
        senão se v == "Superhumano" então
            module.FireRemotes("BuySuperhuman")
        senão se v == "Passo da Morte" então
            module.FireRemotes("BuyDeathStep")
        senão se v == "Garra Elétrica" ​​então
            module.FireRemotes("BuyElectricClaw")
        senão se v == "Sharkman Karate" então
            module.FireRemotes("BuySharkmanKarate")
        senão se v == "Garra de Dragão" então
            module.FireRemotes("BuyDragonTalon")
        senão se v == "Deushumano" então
            module.FireRemotes("BuyGodhuman")
        senão se v == "Arte Sanguínea" então
            module.FireRemotes("BuySanguineArt",true)
            module.FireRemotes("BuySanguineArt")
        fim
    fim
})
local AutoBuyHaki = ShopTab:AddToggle("Comprar automaticamente Haki Spawn", {
    Título = "Compra Automática de Haki Spawn",
    Padrão = Configurações["Comprar Haki Spawn automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Compra automática de Haki Spawn"] = v
        module.Save()
    fim
})
local AutoBuyLegendary = ShopTab:AddToggle("Compra automática de espada lendária", {
    Título = "Compra automática de espada lendária",
    Padrão = Configurações["Comprar Espada Lendária Automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Compra automática de espada lendária"] = v
        module.Save()
    fim
})
ShopTab:AddButton({
    Título = "Estatísticas de reembolso",
    Callback = função()
        CommF_:InvokeServer("BlackbeardReward","Refund","1")
        CommF_:InvokeServer("BlackbeardReward","Refund","2")
    fim
})

local StatusTab = Window:AddTab({ Title = "Servidores de Status", Icon = "rbxassetid://122223674767625" })
StatusTab:AddSection("Status")
local CakePrinceStatus = StatusTab:AddParagraph({ Title = "Status do Príncipe do Bolo", Content = "Apenas Mar 3" })
local EliteStatus = StatusTab:AddParagraph({ Title = "Status Elite", Content = "Apenas Sea 3" })
local LeviathanStatus = StatusTab:AddParagraph({ Title = "Status do Leviatã", Content = "Apenas Mar 3" })
local MirageStatus = StatusTab:AddParagraph({ Title = "Status da Miragem", Content = "Apenas Mar 3" })
local BerriesCheck = StatusTab:AddParagraph({ Title = "Verificação de frutas vermelhas", Content = "Apenas Sea 3" })

StatusTab:AddSection("Servidor")
local JobIdInput = StatusTab:AddInput("ID do Trabalho", {
    Título = "ID da vaga",
    Espaço reservado = "Insira o ID da vaga aqui..."
    Callback = function(v)
        getgenv().JobId = v
    fim
})
StatusTab:AddButton({
    Título = "Junte-se ao ID da vaga",
    Callback = função()
        game.ReplicatedStorage.__ServerBrowser:InvokeServer("teleport", getgenv().JobId)
    fim
})
StatusTab:AddButton({
    Título = "Copiar ID do Trabalho",
    Callback = função()
        setclipboard(game.JobId)
        Fluent:Notify({ Title = "Status dos Servidores", Content = "Cópia Concluída com Sucesso!", Duration = 4 })
    fim
})
StatusTab:AddButton({
    Título = "Reconectar ao servidor",
    Callback = função()
        game.ReplicatedStorage.__ServerBrowser:InvokeServer("teleport", game.JobId)
    fim
})
StatusTab:AddButton({
    Título = "Servidor de Salto",
    Callback = função()
        module.HopServers(10)
    fim
})
StatusTab:AddButton({
    Título = "Servidor Hop com poucos jogadores",
    Callback = função()
        módulo.HopLow()
    fim
})

local ConfigTab = Window:AddTab({ Title = "Config Farm", Icon = "rbxassetid://127147149367603" })
local HopOptions = ConfigTab:AddToggle("Opções de Salto", {
    Título = "Opções de Salto",
    Descrição = "Servidor de troca automática se não houver inimigos ou itens, através de uma verificação de função."
    Padrão = Configurações["Opções de salto"] ou falso,
    Callback = function(v)
        Configurações["Opções de salto"] = v
        module.Save()
    fim
})
local AutoBuso = ConfigTab:AddToggle("Auto Buso", {
    Título = "Auto Buso",
    Descrição = "Ativar automaticamente buso haki",
    Padrão = Configurações["Auto Buso"] ou falso,
    Callback = function(v)
        Configurações["Auto Buso"] = v
        módulo.AutoBuso(v)
        module.Save()
    fim
})
local AutoAwakeningV4 = ConfigTab:AddToggle("Auto Awakening V4", {
    Título = "Auto Awakening V4",
    Descrição = "Corrida automática de curvas v4",
    Padrão = Configurações["Auto Awakening V4"] ou falso,
    Callback = function(v)
        Configurações["Despertar Automático V4"] = v
        module.AutoAwak(v)
        module.Save()
    fim
})
local SafeMode = ConfigTab:AddToggle("Modo Seguro", {
    Título = "Modo de segurança",
    Descrição = "Mesmo Y quando sua saúde estiver baixa",
    Padrão = Configurações["Modo de segurança"] ou falso,
    Callback = function(v)
        Configurações["Modo de segurança"] = v
        module.Save()
    fim
})

ConfigTab:AddSection("Opções de Habilidades de Spam")
local UseMelee = ConfigTab:AddToggle("Usar Melee", {
    Título = "Usar Ataque Corpo a Corpo",
    Descrição = "Habilidade de spam corpo a corpo",
    Padrão = Configurações["Usar combate corpo a corpo"] ou falso,
    Callback = function(v)
        Configurações["Usar combate corpo a corpo"] = v
        module.Save()
    fim
})
local MeleeSkills = ConfigTab:AddDropdown("Habilidades de combate corpo a corpo", {
    Título = "Habilidades de Combate Corpo a Corpo",
    Valores = {"Z", "X", "C"},
    Multi = true,
    Padrão = Configurações["Habilidades de Combate Corpo a Corpo"] ou {},
    Callback = function(v)
        local sel = {}
        para k, em próximo, v faça se em então tabela.inserir(sel, k) fim fim
        Configurações["Habilidades de Combate Corpo a Corpo"] = tabela.concat(sel, " ")
        module.Save()
    fim
})
local UseSword = ConfigTab:AddToggle("Usar Espada", {
    Título = "Usar Espada",
    Descrição = "Espada de Habilidade de Spam",
    Padrão = Configurações["Usar Espada"] ou falso,
    Callback = function(v)
        Configurações["Usar Espada"] = v
        module.Save()
    fim
})
local SwordSkills = ConfigTab:AddDropdown("Habilidades de Espada", {
    Título = "Habilidades com Espada",
    Valores = {"Z", "X"},
    Multi = true,
    Padrão = Configurações["Habilidades com Espada"] ou {},
    Callback = function(v)
        local sel = {}
        para k, em próximo, v faça se em então tabela.inserir(sel, k) fim fim
        Configurações["Habilidades com Espada"] = tabela.concat(sel, " ")
        module.Save()
    fim
})
local UseGun = ConfigTab:AddToggle("Usar Arma", {
    Título = "Usar Arma",
    Descrição = "Arma de Habilidade de Spam",
    Padrão = Configurações["Usar Arma"] ou falso,
    Callback = function(v)
        Configurações["Usar Arma"] = v
        module.Save()
    fim
})
local GunSkills = ConfigTab:AddDropdown("Habilidades com armas", {
    Título = "Habilidades com Armas de Fogo",
    Valores = {"Z", "X"},
    Multi = true,
    Padrão = Configurações["Habilidades com Armas"] ou {},
    Callback = function(v)
        local sel = {}
        para k, em próximo, v faça se em então tabela.inserir(sel, k) fim fim
        Configurações["Habilidades com Armas"] = tabela.concat(sel, " ")
        module.Save()
    fim
})
local UseBloxFruit = ConfigTab:AddToggle("Usar Blox Fruit", {
    Título = "Use Blox Fruit",
    Descrição = "Spam Skill Blox Fruit",
    Padrão = Configurações["Usar Blox Fruit"] ou falso,
    Callback = function(v)
        Configurações["Usar Blox Fruit"] = v
        module.Save()
    fim
})
local BloxFruitSkills = ConfigTab:AddDropdown("Habilidades do Blox Fruit", {
    Título = "Habilidades com Blox Fruit",
    Valores = {"Z", "X", "C", "V", "F"},
    Multi = true,
    Padrão = Configurações["Blox Fruit Skills"] ou {},
    Callback = function(v)
        local sel = {}
        para k, em próximo, v faça se em então tabela.inserir(sel, k) fim fim
        Configurações["Habilidades de Blox Fruit"] = tabela.concat(sel, " ")
        module.Save()
    fim
})

local FarmTab = Window:AddTab({ Title = "Aba Agricultura", Icon = "rbxassetid://127561653320876" })
local WeaponType = FarmTab:AddDropdown("Tipo de Arma", {
    Título = "Tipo de Arma",
    Descrição = "Selecione a ferramenta que você usará para a agricultura",
    Valores = {"Corpo a corpo", "Espada", "Arma de fogo"},
    Padrão = Configurações["Tipo de Arma"] ou "Corpo a Corpo",
    Callback = function(v)
        Configurações["Tipo de Arma"] = v
        module.Save()
    fim
})
local FarmMode = FarmTab:AddDropdown("Modo Fazenda", {
    Título = "Modo Fazenda",
    Descrição = "Selecione o modo de cultivo",
    Valores = {"Nível", "Bolo", "Osso"},
    Padrão = Configurações["Modo Fazenda"] ou "Nível",
    Callback = function(v)
        Configurações["Modo Fazenda"] = v
        module.Save()
    fim
})
local StartFarm = FarmTab:AddToggle("Iniciar Fazenda", {
    Título = "Comece a Fazenda",
    Padrão = Configurações["Iniciar Fazenda"] ou falso,
    Callback = function(v)
        Configurações["Iniciar Fazenda"] = v
        module.Save()
    fim
})
local DoubleQuest = FarmTab:AddToggle("Double Quest", {
    Título = "Dupla Missão",
    Padrão = Configurações["Double Quest"] ou falso,
    Callback = function(v)
        Configurações["Double Quest"] = v
        module.Save()
    fim
})
local DragonStormShoot = FarmTab:AddToggle("Dragon Storm Shoot", {
    Título = "Dragon Storm Shoot",
    Descrição = "use a tempestade de dragões para cultivar",
    Padrão = Configurações["Dragon Storm Shoot"] ou falso,
    Callback = function(v)
        Configurações["Dragon Storm Shoot"] = v
        module.Save()
    fim
})
local KillAura = FarmTab:AddToggle("Aura de Morte", {
    Título = "Aura de Morte",
    Descrição = "Elimina automaticamente o monstro mais próximo",
    Padrão = Configurações["Aura de Morte"] ou falso,
    Callback = function(v)
        Configurações["Aura de Morte"] = v
        module.Save()
    fim
})
local AutoTravelDressrosa = FarmTab:AddToggle("Auto Travel Dressrosa", {
    Título = "Viagem de carro em Dressrosa",
    Descrição = "Realizar automaticamente a missão do NPC na prisão para ir para o mar 2",
    Padrão = Configurações["Viagem Automática Dressrosa"] ou falso,
    Callback = function(v)
        Configurações["Viagem Automática Dressrosa"] = v
        module.Save()
    fim
})
local AutoTravelZou = FarmTab:AddToggle("Auto Travel Zou", {
    Título = "Auto Travel Zou",
    Descrição = "Realizar automaticamente a missão do NPC em Clossium para ir ao mar 3",
    Padrão = Configurações["Auto Travel Zou"] ou falso,
    Callback = function(v)
        Configurações["Auto Travel Zou"] = v
        module.Save()
    fim
})

FarmTab:AddSection("Opções de Maestria")
local SelectMasteryType = FarmTab:AddDropdown("Selecione o tipo de domínio", {
    Título = "Selecionar Tipo de Domínio",
    Valores = {"Domínio de Frutas", "Domínio de Armas"},
    Padrão = Configurações["Selecionar Tipo de Domínio"] ou "Domínio de Frutas",
    Callback = function(v)
        Configurações["Selecionar Tipo de Domínio"] = v
        se v == "Domínio de Armas" então
            Notify("Dwac Hub","ENG : You want click when mobs low\nVN : Ban can tu click khi mob yeu mau",7)
        fim
        module.Save()
    fim
})
local SelectSkills = FarmTab:AddDropdown("Selecionar Habilidades", {
    Título = "Selecione Habilidades",
    Valores = {"Z", "X", "C", "V", "F"},
    Multi = true,
    Padrão = Configurações["Selecionar Habilidades"] ou {},
    Callback = function(v)
        local sel = {}
        para k, em próximo, v faça se em então tabela.inserir(sel, k) fim fim
        Configurações["Selecionar Habilidades"] = tabela.concat(sel, " ")
        module.Save()
    fim
})
local LowHealth = FarmTab:AddSlider("Pouca Saúde (%)", {
    Título = "Baixa Saúde (%)",
    Descrição = "Define a porcentagem de vida como baixa para o mob",
    Mín. = 5,
    Máx. = 100,
    Arredondamento = 1,
    Padrão = Configurações["Saúde Baixa (%)"] ou 30,
    Callback = function(v)
        Configurações["Saúde baixa (%)"] = v
        module.Save()
    fim
})
local FarmMastery = FarmTab:AddToggle("Domínio da Fazenda", {
    Título = "Domínio da Fazenda",
    Descrição = "Comece a dominar a agricultura",
    Padrão = Configurações["Domínio da Fazenda"] ou falso,
    Callback = function(v)
        Configurações["Domínio da Fazenda"] = v
        module.Save()
    fim
})

FarmTab:AddSection("Baú")
local TotalChestClaimed = FarmTab:AddParagraph({ Title = "Total de Baús Reivindicados", Content = "0" })
local AutoChest = FarmTab:AddToggle("Auto Chest", {
    Título = "Baú Automático",
    Padrão = Configurações["Baú Automático"] ou falso,
    Callback = function(v)
        Configurações["Baú Automático"] = v
        module.Save()
    fim
})
local ChestCountsDropdown = FarmTab:AddDropdown("Contagem de Baús", {
    Título = "Contagem de Peitos",
    Valores = {"15", "20", "25", "30", "35"},
    Padrão = Configurações["Contagem de Peitos"] ou "20",
    Callback = function(v)
        Configurações["Contagem de Peitos"] = v
        module.Save()
    fim
})
local AutoChestHop = FarmTab:AddToggle("Auto Chest Hop", {
    Título = "Salto Automático no Peito",
    Padrão = Configurações["Salto Automático no Baú"] ou falso,
    Callback = function(v)
        Configurações["Salto Automático no Peito"] = v
        module.Save()
    fim
})

FarmTab:AddSection("Materiais")
local TodosOsMateriais = {
    "Angel Swings", "Leather", "Sucata Metálica", "Magma Ore", "Fish Tail",
    "Ectoplasma", "Gotícula Mística", "Material Radioativo", "Presa de Vampiro",
    "Cacau Conjurado", "Escama de Dragão", "Pólvora", "Mini Presa"
}
local SelectMaterials = FarmTab:AddDropdown("Selecionar Materiais", {
    Título = "Selecionar Materiais",
    Valores = Todos os Materiais,
    Padrão = Configurações["Selecionar Materiais"] ou "",
    Callback = function(v)
        Configurações["Selecionar Materiais"] = v
        module.Save()
    fim
})
local AutoMaterial = FarmTab:AddToggle("Auto Material", {
    Título = "Material Automotivo",
    Descrição = "Material agrícola automático selecionado",
    Padrão = Configurações["Material Automático"] ou falso,
    Callback = function(v)
        Configurações["Material automático"] = v
        module.Save()
    fim
})

FarmTab:AddSection("Opções do Chefe")
local SelectBoss = FarmTab:AddDropdown("Selecionar Chefe", {
    Título = "Selecione o Chefe",
    Valores = {},
    Padrão = Configurações["Selecionar Chefe"] ou "",
    Callback = function(v)
        Configurações["Selecionar Chefe"] = v
        module.Save()
    fim
})
local RefreshBoss = FarmTab:AddButton({
    Título = "Atualizar Chefe",
    Callback = função()
        listaDeChefesLocais = {}
        para r,v em pares(módulo.Chefes) faça
            se module.VerifyEnemies(r, true) então
                table.insert(bossesList, r)
            fim
        fim
        se #bossesList == 0 então
            bossesList = {"deo co boss"}
        fim
        SelectBoss:SetValues(bossesList)
    fim
})
local TakeQuests = FarmTab:AddToggle("Aceitar Missões", {
    Título = "Aceite Missões",
    Descrição = "Aceitar missão automaticamente após derrotar o chefe"
    Padrão = Configurações["Aceitar missões"] ou falso,
    Callback = function(v)
        Configurações["Aceitar Missões"] = v
        module.Save()
    fim
})
local AutoBoss = FarmTab:AddToggle("Auto Boss", {
    Título = "Auto Boss",
    Descrição = "Eliminar automaticamente o chefe selecionado"
    Padrão = Configurações["Auto Boss"] ou falso,
    Callback = function(v)
        Configurações["Auto Boss"] = v
        module.Save()
    fim
})
local AutoAllBoss = FarmTab:AddToggle("Auto All Boss", {
    Título = "Auto All Boss",
    Descrição = "Eliminar automaticamente todos os chefes vivos no servidor"
    Padrão = Configurações["Automático para todos os chefes"] ou falso,
    Callback = function(v)
        Configurações["Auto All Boss"] = v
        module.Save()
    fim
})

FarmTab:AddSection("Opções de Espada")
local AutoFarmMasteryAllSwords = FarmTab:AddToggle("Auto Farming 600 Mastery All Swords", {
    Título = "Fazenda Automática de Espadas com Maestria 600"
    Descrição = "Gerencia automaticamente todas as espadas em seu inventário com mais de 600 de maestria e trocará por uma nova espada quando a última tiver maestria superior a 600."
    Padrão = Configurações["Auto Farming 600 Maestria Todas as Espadas"] ou falso,
    Callback = function(v)
        Configurações["Auto Farming 600 Maestria Todas as Espadas"] = v
        module.Save()
    fim
})

local StackTab = Window:AddTab({ Title = "Stack Farming", Icon = "rbxassetid://72448332143088" })
StackTab:AddSection("Frutas Vermelhas")
local AutoCollectBerries = StackTab:AddToggle("Coleta automática de frutas vermelhas", {
    Título = "Coleta automática de frutas vermelhas",
    Descrição = "Coleta automática de frutas silvestres geradas na área de trabalho"
    Padrão = Configurações["Coleta automática de frutas"] ou falso,
    Callback = function(v)
        Configurações["Coleta automática de frutas"] = v
        module.Save()
    fim
})
local AutoCollectBerriesHop = StackTab:AddToggle("Coletar automaticamente frutas [HOP]", {
    Título = "Coleta automática de frutas vermelhas [HOP]",
    Padrão = Configurações["Coleta automática de frutas vermelhas Hop"] ou falso,
    Callback = function(v)
        Configurações["Coleta automática de frutas vermelhas Hop"] = v
        module.Save()
    fim
})

StackTab:AddSection("Tiki Outpost")
local AutoTyrant = StackTab:AddToggle("Auto Tyrant dos céus", {
    Título = "Auto Tirano dos Céus",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Tirano dos céus"] ou falso,
    Callback = function(v)
        Configurações["Auto Tirano dos céus"] = v
        module.Save()
    fim
})

StackTab:AddSection("Função Pilhas")
local AutoEliteHunter = StackTab:AddToggle("Auto Elite Hunter", {
    Título = "Auto Elite Hunter",
    Descrição = "Missão de reivindicação automática e eliminação de monstros de elite",
    Padrão = Configurações["Auto Elite Hunter"] ou falso,
    Callback = function(v)
        Configurações["Auto Elite Hunter"] = v
        module.Save()
    fim
})
local AutoEliteHunterHop = StackTab:AddToggle("Auto Elite Hunter [HOP]", {
    Título = "Auto Elite Hunter [HOP]",
    Padrão = Configurações["Auto Elite Hunter Hop"] ou falso,
    Callback = function(v)
        Configurações["Auto Elite Hunter Hop"] = v
        module.Save()
    fim
})
local AutoCastleRaid = StackTab:AddToggle("Auto Castle Raid", {
    Título = "Auto Castle Raid",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Ataque Automático ao Castelo"] ou falso,
    Callback = function(v)
        Configurações["Ataque Automático ao Castelo"] = v
        module.Save()
    fim
})
local AutoFactory = StackTab:AddToggle("Auto Factory", {
    Título = "Fábrica de Automóveis",
    Descrição = "Somente função Sea 2",
    Padrão = Configurações["Auto Factory"] ou falso,
    Callback = function(v)
        Configurações["Auto Factory"] = v
        module.Save()
    fim
})
local AutoDarkbeard = StackTab:AddToggle("Auto Darkbeard", {
    Título = "Auto Darkbeard",
    Descrição = "Somente função Sea 2",
    Padrão = Configurações["Auto Darkbeard"] ou falso,
    Callback = function(v)
        Configurações["Auto Darkbeard"] = v
        module.Save()
    fim
})
local AutoAdmin = StackTab:AddToggle("Auto Admin", {
    Título = "Administração Automática",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Administração Automática"] ou falso,
    Callback = function(v)
        Configurações["Administração Automática"] = v
        module.Save()
    fim
})
local AutoDoughKing = StackTab:AddToggle("Auto Dough King", {
    Título = "Auto Dough King",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Dough King"] ou falso,
    Callback = function(v)
        Configurações["Auto Dough King"] = v
        module.Save()
    fim
})

local ItemsTab = Window:AddTab({ Title = "Cultivo de Itens", Icon = "rbxassetid://97087268377873" })
ItemsTab:AddSection("Espadas")
local AutoSaber = ItemsTab:AddToggle("AutoSaber", {
    Título = "Auto Saber",
    Descrição = "Função Somente Mar 1",
    Padrão = Configurações["Auto Saber"] ou falso,
    Callback = function(v)
        Configurações["Auto Saber"] = v
        module.Save()
    fim
})
local AutoPole = ItemsTab:AddToggle("Auto Pole (1ª forma)", {
    Título = "Auto Pole (1ª forma)",
    Descrição = "Função Somente Mar 1",
    Padrão = Configurações["Pole Automático (1ª forma)"] ou falso,
    Callback = function(v)
        Configurações["Pole Automático (1ª forma)"] = v
        module.Save()
    fim
})
local AutoRengoku = ItemsTab:AddToggle("Auto Rengoku", {
    Título = "Auto Rengoku",
    Descrição = "Somente função Sea 2",
    Padrão = Configurações["Auto Rengoku"] ​​ou falso,
    Callback = function(v)
        Configurações["Auto Rengoku"] ​​= v
        module.Save()
    fim
})
local AutoYama = ItemsTab:AddToggle("Auto Yama", {
    Título = "Auto Yama",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Yama"] ou falso,
    Callback = function(v)
        Configurações["Auto Yama"] = v
        module.Save()
    fim
})
local AutoTushita = ItemsTab:AddToggle("Auto Tushita", {
    Título = "Auto Tushita",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Tushita"] ou falso,
    Callback = function(v)
        Configurações["Auto Tushita"] = v
        module.Save()
    fim
})
local AutoHallowScythe = ItemsTab:AddToggle("Auto Hallow Scythe", {
    Título = "Foice Automática Hallow",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Hallow Scythe"] ou falso,
    Callback = function(v)
        Configurações["Auto Hallow Scythe"] = v
        module.Save()
    fim
})
local AutoCDK = ItemsTab:AddToggle("Auto Dual Cursed Katana", {
    Título = "Katana Amaldiçoada Dupla Automática",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Dual Cursed Katana"] ou falso,
    Callback = function(v)
        Configurações["Auto Dual Cursed Katana"] = v
        module.Save()
    fim
})

ItemsTab:AddSection("Combate Corpo a Corpo")
local AutoSuperhuman = ItemsTab:AddToggle("Auto Superhuman", {
    Título = "Auto Superhumano",
    Descrição = "Suporte de função para todos os mares",
    Padrão = Configurações["Auto Superhuman"] ou falso,
    Callback = function(v)
        Configurações["Auto Superhuman"] = v
        module.Save()
    fim
})
local AutoDeathStep = ItemsTab:AddToggle("Passo de Morte Automático", {
    Título = "Passo de Morte Automática",
    Descrição = "Somente função Sea 2",
    Padrão = Configurações["Passo de Morte Automático"] ou falso,
    Callback = function(v)
        Configurações["Passo de Morte Automático"] = v
        module.Save()
    fim
})
local AutoSharkman = ItemsTab:AddToggle("Auto Sharkman Karatê", {
    Título = "Caratê Automático do Homem-Tubarão",
    Descrição = "Somente função Sea 2",
    Padrão = Configurações["Auto Sharkman Karate"] ou falso,
    Callback = function(v)
        Configurações["Auto Sharkman Karate"] = v
        module.Save()
    fim
})
local AutoElectricClaw = ItemsTab:AddToggle("Garra Elétrica Automática", {
    Título = "Garra Elétrica Automática",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Garra Elétrica Automática"] ou falso,
    Callback = function(v)
        Configurações["Garra Elétrica Automática"] = v
        module.Save()
    fim
})
local AutoDragonTalon = ItemsTab:AddToggle("Auto Dragon Talon", {
    Título = "Auto Dragon Talon",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Dragon Talon"] ou falso,
    Callback = function(v)
        Configurações["Auto Dragon Talon"] = v
        module.Save()
    fim
})
local AutoGodhuman = ItemsTab:AddToggle("Auto Godhuman", {
    Título = "Auto Godhuman",
    Descrição = "Para obter o Godhuman, você precisa dominar todos os estilos de luta v2 (Super-humano, Passo da Morte, Karatê do Homem-Tubarão, Garra Elétrica, Garra de Dragão) e ter mais de 400 pontos de maestria."
    Padrão = Configurações["Auto Godhuman"] ou falso,
    Callback = function(v)
        Configurações["Auto Godhuman"] = v
        module.Save()
    fim
})

ItemsTab:AddSection("Arma")
local AutoSoulGuitar = ItemsTab:AddToggle("Auto Soul Guitar", {
    Título = "Auto Soul Guitar",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Auto Soul Guitar"] ou falso,
    Callback = function(v)
        Configurações["Auto Soul Guitar"] = v
        module.Save()
    fim
})

local FruitsTab = Window:AddTab({ Title = "Frutas e Raid", Icon = "rbxassetid://119340207028601" })
AbaFrutas:AdicionarSeção("Frutas")
AbaFrutas:AdicionarBotão({
    Título = "Frutas Aleatórias",
    Callback = função()
        module.FireRemotes("Primo", "Comprar")
    fim
})
local AutoRollFruits = FruitsTab:AddToggle("Rolar frutas automaticamente", {
    Título = "Frutas de Rolagem Automática",
    Padrão = Configurações["Rolar Frutas Automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Rolar Frutas Automaticamente"] = v
        module.Save()
    fim
})
local TweenFruitSpawn = FruitsTab:AddToggle("Tween para Gerar Frutas", {
    Título = "Do pré-adolescente ao nascimento de frutos",
    Padrão = Configurações["Interpolação para Germinação de Frutas"] ou falso,
    Callback = function(v)
        Configurações["Interpolação para Germinação de Frutas"] = v
        module.Save()
    fim
})
local StoreFruits = FruitsTab:AddToggle("Armazenar frutas", {
    Título = "Armazene frutas",
    Padrão = Configurações["Armazenar frutas"] ou falso,
    Callback = function(v)
        Configurações["Armazenar frutas"] = v
        module.Save()
    fim
})

AbaFrutas:AdicionarSeção("Invasão")
local SelectRaid = FruitsTab:AddDropdown("Selecionar Raid", {
    Título = "Selecionar Raid",
    Valores = {"Chama", "Gelo", "Terremoto", "Luz", "Escuridão", "Aranha", "Estrondo", "Magma", "Buda", "Areia", "Fênix", "Massa"},
    Padrão = Configurações["Selecionar Raide"] ou "Chama",
    Callback = function(v)
        Configurações["Selecionar Raid"] = v
        module.Save()
    fim
})
AbaFrutas:AdicionarBotão({
    Título = "Comprar Chip",
    Callback = função()
        module.FireRemotes("RaidsNpc", "Select", (Settings["Select Raid"] or "Flame"))
    fim
})
local StartRaid = FruitsTab:AddToggle("Iniciar Raid", {
    Título = "Iniciar Raid",
    Padrão = Configurações["Iniciar Raid"] ou falso,
    Callback = function(v)
        Configurações["Iniciar Raid"] = v
        module.Save()
    fim
})
local KillRaid = FruitsTab:AddToggle("Kill Raid", {
    Título = "Ataque de Eliminação",
    Descrição = "Elimina automaticamente o inimigo mais próximo durante uma incursão",
    Padrão = Configurações["Kill Raid"] ou falso,
    Callback = function(v)
        Configurações["Ataque de Matança"] = v
        module.Save()
    fim
})
local NextIslands = FruitsTab:AddToggle("Next Islands", {
    Título = "Próximas Ilhas",
    Descrição = "Ataque automático às próximas ilhas",
    Padrão = Configurações["Próximas Ilhas"] ou falso,
    Callback = function(v)
        Configurações["Próximas Ilhas"] = v
        module.Save()
    fim
})
local AutoAwaken = FruitsTab:AddToggle("Auto Awaken", {
    Título = "Despertar Automático",
    Padrão = Configurações["Ativar automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Ativação automática"] = v
        module.Save()
    fim
})

local PlayerTab = Window:AddTab({ Title = "Local Player", Icon = "rbxassetid://98870151777863" })
PlayerTab:AddButton({
    Título = "Teletransporte para o Principal (Mar 1)",
    Callback = função()
        module.TeleportWorld(1)
    fim
})
PlayerTab:AddButton({
    Título = "Teletransporte para Dressrosa (Sea 2)",
    Callback = função()
        module.TeleportWorld(2)
    fim
})
PlayerTab:AddButton({
    Título = "Teletransporte para Zou (Mar 3)",
    Callback = função()
        module.TeleportWorld(3)
    fim
})

listaDeJogadores local = {}
para _,v em próximo, jogo.Jogadores:ObterJogadores() faça
    se v.Name ~= plr.Name então
        table.insert(PlayerList, v.Name)
    fim
fim

local SelectStats = PlayerTab:AddDropdown("Selecionar Estatísticas", {
    Título = "Selecionar Estatísticas",
    Valores = {"Corpo a corpo", "Defesa", "Arma de fogo", "Fruta do Demônio"},
    Padrão = Configurações["Selecionar Estatísticas"] ou "Corpo a Corpo",
    Callback = function(v)
        Configurações["Selecionar Estatísticas"] = v
        module.Save()
    fim
})
local AutoStats = PlayerTab:AddToggle("Auto Stats", {
    Título = "Estatísticas Automáticas",
    Padrão = Configurações["Estatísticas Automáticas"] ou falso,
    Callback = function(v)
        Configurações["Estatísticas Automáticas"] = v
        module.AutoStats(v)
        module.Save()
    fim
})

local SelectPlayers = PlayerTab:AddDropdown("Selecionar Jogadores", {
    Título = "Selecione os jogadores",
    Valores = Lista de Jogadores,
    Padrão = "",
    Callback = function(v)
        getgenv().SelectPlayers = v
    fim
})
PlayerTab:AddButton({
    Título = "Atualizar Jogadores",
    Callback = função()
        local newList = {}
        para _,v em próximo, jogo.Jogadores:ObterJogadores() faça
            se v.Name ~= plr.Name então
                tabela.inserir(novaLista, v.Nome)
            fim
        fim
        SelectPlayers:SetValues(newList)
    fim
})
local TeleportToPlayers = PlayerTab:AddToggle("Teleport To Players", {
    Título = "Teletransporte para Jogadores",
    Padrão = Configurações["Teletransportar para Jogadores"] ou falso,
    Callback = function(v)
        Configurações["Teletransportar para Jogadores"] = v
        module.Save()
    fim
})
local JogadoresEspectadores = PlayerTab:AddToggle("Jogadores Espectadores", {
    Título = "Jogadores Espectadores",
    Padrão = Configurações["Espectar jogadores"] ou falso,
    Callback = function(v)
        Configurações["Jogadores Espectadores"] = v
        se v então
            Se workspace.Characters:FindFirstChild(getgenv().SelectPlayers) então
                workspace.Camera.CameraSubject = workspace.Characters[getgenv().SelectPlayers]
            fim
        outro
            workspace.Camera.CameraSubject = plr.Character
        fim
        module.Save()
    fim
})
local WalkSpeedToggle = PlayerTab:AddToggle("WalkSpeed", {
    Título = "Velocidade de Caminhada",
    Descrição = "Ativar limite de velocidade de caminhada",
    Padrão = Configurações["AlternarVelocidadeDeCaminhada"] ou falso,
    Callback = function(v)
        Configurações["AlternarVelocidadeDeCaminhada"] = v
        module.Save()
    fim
})
local WalkSpeedValue = PlayerTab:AddSlider("Velocidade de Caminhada", {
    Título = "Velocidade de Caminhada",
    Mín. = 50,
    Máx. = 350,
    Arredondamento = 1,
    Padrão = Configurações["Velocidade de Caminhada"] ou 150,
    Callback = function(v)
        Configurações["WalkSpeed"] = v
        getgenv().WalkSpeed ​​= v
        module.Save()
    fim
})
local InfinityRange = PlayerTab:AddToggle("Infinity Range Observation Haki", {
    Título = "Haki da Observação de Alcance Infinito",
    Padrão = Configurações["Infinity Range Observation Haki"] ou falso,
    Callback = function(v)
        Configurações["Haki de Observação de Alcance Infinito"] = v
        se não v e RangeOld então
            game:GetService("Players").LocalPlayer.VisionRadius.Value = RangeOld
        fim
        module.Save()
    fim
})

local PVPTab = Window:AddTab({ Title = "PVP-Combat", Icon = "rbxassetid://125736686613291" })
local TargetSelect = PVPTab:AddDropdown("Selecionar alvo", {
    Título = "Selecionar Alvo",
    Valores = Lista de Jogadores,
    Padrão = "",
    Callback = function(v)
        getgenv().TargetSelect = v
    fim
})
PVPTab:AddButton({
    Título = "Atualizar alvo",
    Callback = função()
        local newList = {}
        para _,v em próximo, jogo.Jogadores:ObterJogadores() faça
            se v.Name ~= plr.Name então
                tabela.inserir(novaLista, v.Nome)
            fim
        fim
        TargetSelect:SetValues(newList)
    fim
})
local AimbotSkills = PVPTab:AddToggle("Habilidades Aimbot", {
    Título = "Habilidades de Aimbot",
    Padrão = Configurações["Habilidades de Aimbot"] ou falso,
    Callback = function(v)
        Configurações["Habilidades de Aimbot"] = v
        module.Save()
    fim
})


local VolcanoTab = Window:AddTab({ Title = "Eventos do Vulcão", Icon = "rbxassetid://71385541823712" })
local PrehistoricStatus = VolcanoTab:AddParagraph({ Title = "Ilha Pré-histórica", Content = "Não Gerada" })
local AutoFindPrehistoric = VolcanoTab:AddToggle("Localizar Ilha Pré-histórica Automaticamente", {
    Título = "Localização automática de ilha pré-histórica",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Localizar Ilha Pré-histórica Automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Localizar Ilha Pré-histórica Automaticamente"] = v
        module.Save()
    fim
})
local AutoPrehistoric = VolcanoTab:AddToggle("Auto Prehistoric Island", {
    Título = "Ilha Pré-histórica Automotiva",
    Descrição = "iniciar automaticamente o evento Vocalon e destruir rochas na ilha"
    Padrão = Configurações["Automático Ilha Pré-histórica"] ou falso,
    Callback = function(v)
        Configurações["Auto Ilha Pré-histórica"] = v
        module.Save()
    fim
})
local AutoLavaGolem = VolcanoTab:AddToggle("Auto Lava Golem", {
    Título = "Auto Lava Golem",
    Descrição = "Morrer lava automaticamente",
    Padrão = Configurações["Auto Lava Golem"] ou falso,
    Callback = function(v)
        Configurações["Golem de Lava Automático"] = v
        module.Save()
    fim
})
local AutoCollectDinoBone = VolcanoTab:AddToggle("Coletar automaticamente osso de dinossauro", {
    Título = "Coleta Automática de Ossos de Dinossauro",
    Descrição = "Pré-histórico",
    Padrão = Configurações["Coleta automática de ossos de dinossauro"] ou falso,
    Callback = function(v)
        Configurações["Coleta automática de osso de dinossauro"] = v
        module.Save()
    fim
})
local AutoCollectDragonEgg = VolcanoTab:AddToggle("Coletar automaticamente ovo de dragão", {
    Título = "Coleta Automática de Ovos de Dragão",
    Descrição = "Pré-histórico",
    Padrão = Configurações["Coleta automática de ovos de dragão"] ou falso,
    Callback = function(v)
        Configurações["Coleta automática de ovos de dragão"] = v
        module.Save()
    fim
})


local SeaTab = Window:AddTab({ Title = "Eventos Marítimos", Icon = "rbxassetid://96788654458681" })
SeaTab:AddButton({
    Título = "Sem Sapo",
    Callback = função()
        Se game:GetService("Lighting"):FindFirstChild("LightingLayers") então
            game:GetService("Lighting"):FindFirstChild("LightingLayers"):Destroy()
        fim
    fim
})
local SelectBoats = SeaTab:AddDropdown("Selecionar barcos", {
    Título = "Selecione Barcos",
    Valores = {"Guardião", "Bote", "Chapela Pirata", "Brigada Pirata", "Grande Brigada Pirata", "Chapela da Marinha", "Brigada da Marinha", "Grande Brigada da Marinha", "Caçador de Feras"},
    Padrão = Configurações["Selecionar barcos"] ou "Guardian",
    Callback = function(v)
        Configurações["Selecionar barcos"] = v
        module.Save()
    fim
})
SeaTab:AddButton({
    Título = "Teletransporte-se para o seu barco local",
    Callback = função()
        Se module.GetLocalBoat() então
            module.Tweento(module.GetLocalBoat().VehicleSeat.CFrame*CFrame.new(0,2,0))
        fim
    fim
})
local EnableSpeedBoats = SeaTab:AddToggle("Ativar Lanchas Rápidas", {
    Título = "Permitir lanchas rápidas",
    Padrão = Configurações["Ativar lanchas"] ou falso,
    Callback = function(v)
        Configurações["Ativar lanchas"] = v
        module.Save()
    fim
})
local BoatSpeed ​​= SeaTab:AddSlider("Velocidade do barco", {
    Título = "Velocidade do barco",
    Mín. = 180,
    Máx. = 400,
    Arredondamento = 1,
    Padrão = Configurações["Velocidade do Barco"] ou 260,
    Callback = function(v)
        Configurações["Velocidade do barco"] = v
        module.Save()
    fim
})
local SelectZone = SeaTab:AddDropdown("Selecionar Zona", {
    Título = "Selecionar Zona",
    Valores = {"Zona 1", "Zona 2", "Zona 3", "Zona 4", "Zona 5", "Zona 6", "Infinito"},
    Padrão = Configurações["Selecionar Zona"] ou "Zona 1",
    Callback = function(v)
        Configurações["Selecionar Zona"] = v
        module.Save()
    fim
})
local StartSeaEvents = SeaTab:AddToggle("Iniciar eventos automáticos do mar", {
    Título = "Iniciar eventos marítimos automáticos",
    Padrão = Configurações["Iniciar eventos automáticos do mar"] ou falso,
    Callback = function(v)
        Configurações["Iniciar eventos marítimos automáticos"] = v
        module.Save()
    fim
})
local AutoSharkFish = SeaTab:AddToggle("Membro da Tripulação Automática de Tubarões e Peixes", {
    Título = "Membro da Equipe Auto Shark and Fish",
    Padrão = Configurações["Membro automático da tripulação de tubarão e peixe"] ou falso,
    Callback = function(v)
        Configurações["Membro da Tripulação Automática de Tubarões e Peixes"] = v
        module.Save()
    fim
})
local AutoTerrorShark = SeaTab:AddToggle("Auto Terror Shark", {
    Título = "Tubarão do Terror Automático",
    Padrão = Configurações["Auto Terror Shark"] ou falso,
    Callback = function(v)
        Configurações["Auto Terror Shark"] = v
        module.Save()
    fim
})
local AutoPiratesShip = SeaTab:AddToggle("Auto Pirate Ship", {
    Título = "Navio Pirata Automático",
    Padrão = Configurações["Auto Pirate Ship"] ou falso,
    Callback = function(v)
        Configurações["Navio Pirata Automático"] = v
        se v então
            Fluent:Notify({ Title = "Aviso de Script", Content = "Selecione Habilidades na Aba de Configuração da Fazenda", Duration = 8 })
        fim
        module.Save()
    fim
})
local AutoGhostShip = SeaTab:AddToggle("Auto Ghost Ship", {
    Título = "Auto Ghost Ship",
    Padrão = Configurações["Auto Ghost Ship"] ou falso,
    Callback = function(v)
        Configurações["Auto Ghost Ship"] = v
        se v então
            Fluent:Notify({ Title = "Aviso de Script", Content = "Selecione Habilidades na Aba de Configuração da Fazenda", Duration = 8 })
        fim
        module.Save()
    fim
})
local AutoSeaBeast = SeaTab:AddToggle("Auto Sea Beast", {
    Título = "Auto Sea Beast",
    Padrão = Configurações["Auto Sea Beast"] ou falso,
    Callback = function(v)
        Configurações["Auto Sea Beast"] = v
        se v então
            Fluent:Notify({ Title = "Aviso de Script", Content = "Selecione Habilidades na Aba de Configuração da Fazenda", Duration = 8 })
        fim
        module.Save()
    fim
})
local AutoPiranha = SeaTab:AddToggle("Auto Piranha", {
    Título = "Auto Piranha",
    Padrão = Configurações["Auto Piranha"] ou falso,
    Callback = function(v)
        Configurações["Auto Piranha"] = v
        module.Save()
    fim
})

SeaTab:AddSection("Leviathan")
SeaTab:AddButton({
    Título = "Comprar Spy Leviathan",
    Callback = função()
        module.FireRemotes("InfoLeviathan","2")
    fim
})
SeaTab:AddButton({
    Título = "Caçador de Feras Artesanal",
    Callback = função()
        module.FireRemotes("CraftItem","Check","LeviathanBoat")
        module.FireRemotes("CraftItem","Craft","LeviathanBoat")
    fim
})
local AutoFindLeviathan = SeaTab:AddToggle("Localizar Leviatã automaticamente", {
    Título = "Localização automática de Leviatã",
    Descrição = "Encontrando automaticamente o chefe Leviatã",
    Padrão = Configurações["Localizar Leviatã automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Localizar Leviatã automaticamente"] = v
        module.Save()
    fim
})
local AutoLeviathan = SeaTab:AddToggle("Auto Leviathan", {
    Título = "Auto Leviatã",
    Descrição = "Chefe Leviatã que mata automaticamente",
    Padrão = Configurações["Auto Leviathan"] ou falso,
    Callback = function(v)
        Configurações["Auto Leviathan"] = v
        se v então
            Fluent:Notify({ Title = "Aviso de Script", Content = "Selecione Habilidades na Aba de Configuração da Fazenda", Duration = 8 })
        fim
        module.Save()
    fim
})
local AutoSailToTiki = SeaTab:AddToggle("Auto Sail Boat To Tiki", {
    Título = "Barco à Vela Automático para Tiki",
    Padrão = Configurações["Auto Sail Boat To Tiki"] ou falso,
    Callback = function(v)
        Configurações["Auto Sail Boat To Tiki"] = v
        module.Save()
    fim
})

SeaTab:AddSection("Eventos Kitsune")
local AutoFindKitsune = SeaTab:AddToggle("Localizar automaticamente a Ilha Kitsune", {
    Título = "Localização automática da Ilha Kitsune",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Localizar Ilha Kitsune automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Localizar automaticamente a Ilha Kitsune"] = v
        module.Save()
    fim
})
local AutoCollectAzure = SeaTab:AddToggle("Coleta automática de membros do Azure", {
    Título = "Coleta automática de membros do Azure",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Coletar automaticamente membros do Azure"] ou falso,
    Callback = function(v)
        Configurações["Coletar automaticamente membro do Azure"] = v
        module.Save()
    fim
})
local AutoTradeAzure = SeaTab:AddToggle("Membro do Auto Trade Azure", {
    Título = "Membro do Auto Trade Azure",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Membro do Azure de negociação automática"] ou falso,
    Callback = function(v)
        Configurações["Membro do Azure de negociação automática"] = v
        module.Save()
    fim
})

local DojoTab = Window:AddTab({ Title = "Dojo", Icon = "rbxassetid://91920478152016" })
local AutoDojoTrainer = DojoTab:AddToggle("Auto Dojo Trainer", {
    Título = "Auto Dojo Trainer",
    Padrão = Configurações["Auto Dojo Trainer"] ou falso,
    Callback = function(v)
        Configurações["Auto Dojo Trainer"] = v
        module.Save()
    fim
})
local AutoBlazeEmbers = DojoTab:AddToggle("Auto Blaze Embers", {
    Título = "Auto Blaze Embers",
    Padrão = Configurações["Auto Blaze Embers"] ou falso,
    Callback = function(v)
        Configurações["Auto Blaze Embers"] = v
        module.Save()
    fim
})
DojoTab:AddButton({
    Título = "Craft Dragon Storm",
    Callback = função()
        module.FireRemotes("CraftItem","Check","Dragonstorm")
        module.FireRemotes("CraftItem","Craft","Dragonstorm")
    fim
})
DojoTab:AddButton({
    Título = "Artesanato do Coração do Dragão",
    Callback = função()
        module.FireRemotes("CraftItem","Check","Dragonheart")
        module.FireRemotes("CraftItem","Craft","Dragonheart")
    fim
})


local RaceTab = Window:AddTab({ Title = "Raça Aprimorada", Icon = "rbxassetid://115164375298022" })
RaceTab:AddSection("Mirage Puzzle")
local MiragePuzzleStatus = RaceTab:AddParagraph({ Title = "Status do Quebra-Cabeça Mirage", Content = "Não concluído" })
local AutoFindMirage = RaceTab:AddToggle("Localizar Ilha Mirage automaticamente", {
    Título = "Localização automática da Ilha Mirage",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Localizar Ilha Mirage automaticamente"] ou falso,
    Callback = function(v)
        Configurações["Localizar Ilha Mirage automaticamente"] = v
        module.Save()
    fim
})
RaceTab:AddButton({
    Título = "Teletransporte para a Ilha Miragem",
    Descrição = "Somente função Sea 3",
    Callback = função()
        repita task.wait()
            local HighPos = CFrame.new(0,0,0)
            Se module.GetHighPart() então
                HighPos = module.GetHighPart().CFrame * CFrame.new(0, 12, 0)
            elseif WS.Map.MysticIsland then
                HighPos = WS.Map.MysticIsland.WorldPivot * CFrame.new(0, 500, 0)
            fim
            module.Tweento(HighPos)
        até que module.GetDistance(HighPos.Position) <= 50 ou plr.Character.Humanoid.Health <= 0
    fim
})
local AutoPullLever = RaceTab:AddToggle("Alavanca de puxar automática", {
    Título = "Alavanca de acionamento automático",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Alavanca de Puxar Automática"] ou falso,
    Callback = function(v)
        Configurações["Alavanca de acionamento automático"] = v
        module.Save()
    fim
})
local AutoLookAtMoon = RaceTab:AddToggle("Auto Look At Moon", {
    Título = "Olhar Automático para a Lua",
    Descrição = "Somente função Sea 3",
    Padrão = Configurações["Olhar automaticamente para a Lua"] ou falso,
    Callback = function(v)
        Configurações["Olhar automaticamente para a Lua"] = v
        module.Save()
    fim
})
RaceTab:AddButton({
    Título = "Teletransporte para a engrenagem",
    Descrição = "Somente função Sea 3",
    Callback = função()
        local Gear = module.GetGear()
        Se Gear e Gear.Transparency == 0 e não Gear.CanCollide então
            repita task.wait()
                module.Tweento(Gear.CFrame)
            até que não Gear
        fim
    fim
})

RaceTab:AddSection("Corrida Atualizada")
RaceTab:AddParagraph({ Title = "Aguardando atualização", Content = "" })

Mundo = ((game.PlaceId == 2753915549 ou game.PlaceId == 85211729168715) e 1 ou (game.PlaceId == 4442272183 ou game.PlaceId == 79091703265657) e 2 ou (game.PlaceId == 7449423635 ou game.PlaceId == 100117331123089) e 3)
se Mundo == 1 então
    Sea1 = verdadeiro
senão se Mundo == 2 então
    Sea2 = verdadeiro
senão se Mundo == 3 então
    Sea3 = verdadeiro
outro
    plr:Kick("[Dwac Hub]\nDetecção de Jogo Inválido")
fim

ListaDeEntrada = {}
module.GetNearEntrance = function(a)
    local choose = Vector3.new(0, 0, 0)
	local dis = math.huge
    ListaDeEntrada = {
        {
            ["Sky Arena 1"] = Vector3.new(-4654.3046875, 872.5831909179688, -1759.1536865234375),
            ["Sky Arena 2"] = Vector3.new(-7894.6181640625, 5547.14208984375, -380.2909851074219),
            ["UndeyWater City 1"] = Vector3.new(61163.8515625, 11.680007934570312, 1819.7840576171875),
            ["UndeyWater City 2"] = Vector3.new(3864.68798828125, 5.41372013092041, -1926.2139892578125)
        },
        {
            ["Mansão"] = Vector3.new(-288.0594177246094, 305.90118408203125, 613.7842407226562),
            ["Sala do Cisne"] = Vector3.new(2284.96533203125, 15.192192077636719, 897.8220825195312),
            ["Navio de Saída"] = Vector3.new(-6518.1787109375, 83.2271957397461, -145.9620819091797),
            ["No navio"] = Vector3.new(923.448486328125, 125.0971908569336, 32883.55859375)
        },
        {
            ["Mansão"] = Vector3.new(-12550.44921875, 337.20880126953125, -7476.7158203125),
            ["Castelo no Mar"] = Vector3.new(-5073.84912109375, 314.5505676269531, -3152.5322265625),
            ["Ilha da Hidra"] = Vector3.new(5681.67236328125, 1013.0841674804688, -313.3254699707031),
            ["Templo do Tempo"] = Vector3.new(28294.119140625, 14896.5498046875, 103.02708435058594)
        },
    }
	para r, v em pares(EntranceList[World]) faça
		se (v - a.Position).Magnitude < dis e v ~= choose então
			escolher = v
			dis = (v - a.Posição).Magnitude
		fim   
	fim
	retornar escolher
fim

módulo.ObterDistância = função(a, aa)
    se aa == nil então aa = game.Players.LocalPlayer.Character.HumanoidRootPart.Position fim
	se typeof(a) == "CFrame" então
		retornar (a.Posição - aa).Magnitude
	senão se typeof(a) == "Vector3" então
		retornar (a - aa).Magnitude
	fim
fim

Portal local desbloqueado = falso
spawn(function()
    while wait() do
        se CommF_:InvokeServer('GetUnlockables')["DefeatedIndraTrueForm"] então
            PortalDesbloqueado = verdadeiro
        fim
    fim
fim)

module.Entranceto = function(a)
    argumentos locais = {
        "requestEntrance",
        a
    }
    CommF_:InvokeServer(unpack(args))
    plr.Character.PrimaryPart.CFrame = CFrame.new(plr.Character.PrimaryPart.CFrame.X, plr.Character.PrimaryPart.CFrame.Y + 120, plr.Character.PrimaryPart.CFrame.Z)
    task.wait(.1)
fim

module.Tweento = function(ChiTayXinhGai)
    pcall(function()
        se plr.Character e plr.Character:FindFirstChild("Humanoid") e plr.Character.Humanoid.Health > 0 e plr.Character:FindFirstChild("HumanoidRootPart") e plr.Character:FindFirstChild("Head") então
            Distância local = (ChiTayXinhGai.Position - game.Players.LocalPlayer.Character.PrimaryPart.Position).Magnitude
            local TweenService = game:GetService("TweenService")
            Portal local = módulo.GetNearEntrance(ChiTayXinhGai)
            Se a distância for menor ou igual a 200, então
                pcall(function()
                    tween:Cancel()
                fim)
                game.Players.LocalPlayer.Character.PrimaryPart.CFrame = ChiTayXinhGai
            outro
                se (Sea3 e PortalUnlocked ou Sea2 ou Sea1) e Portal e (Portal - ChiTayXinhGai.p).Magnitude + 150 < (game.Players.LocalPlayer.Character.PrimaryPart.Position - ChiTayXinhGai.Position).Magnitude então
                    pcall(function()
                        tween:Cancel()
                    fim)
                    módulo.Entrada(Portal)
                outro
                    tween = TweenService:Create(game.Players.LocalPlayer.Character.PrimaryPart, TweenInfo.new(Distance / 325, Enum.EasingStyle.Linear), {CFrame = ChiTayXinhGai})
                    tween:Play()
                fim
            fim
        fim
    fim)
fim

spawn(function()
    while wait() do
        pcall(function()
            Se NoClip então
                se não game.Players.LocalPlayer.Character.Head:FindFirstChild("Lock") então
                    local Lock = Instance.new("BodyVelocity")
                    Lock.Parent = game.Players.LocalPlayer.Character.Head
                    Lock.Name = "Lock"
                    Lock.MaxForce = Vector3.new(100000, 100000, 100000)
                    Lock.Velocity = Vector3.new(0,0,0)
                    Lock.P = 15000
                fim
                para _,v em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
                    Se v:IsA("BasePart") então
                        v.CanCollide = false
                    fim
                fim
            outro
                Se game.Players.LocalPlayer.Character.Head:FindFirstChild("Lock") então
                    game.Players.LocalPlayer.Character.Head:FindFirstChild("Lock"):Destroy()
                    plr.Character.Humanoid:ChangeState()
                fim
            fim
        fim)
    fim
fim)

module.GetWeaponType = function(x)
	r = ""
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Mochila:ObterFilhos() faça
		se v:IsA("Tool") e v.ToolTip == x então
			r = v.Nome
		fim
	fim
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Personagem:ObterFilhos() faça
		se v:IsA("Tool") e v.ToolTip == x então
			r = v.Nome
		fim
	fim
	retornar r
fim

módulo.ObterArmaAtual = função ()
    r = ""
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Mochila:ObterFilhos() faça
		se v:IsA("Tool") e v.ToolTip == Settings["Weapon Type"] então
			r = v.Nome
		fim
	fim
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Personagem:ObterFilhos() faça
		se v:IsA("Tool") e v.ToolTip == Settings["Weapon Type"] então
			r = v.Nome
		fim
	fim
	retornar r
fim

module.EquipToolName = function(xx)
	ferramenta local = jogo.Jogadores.JogadorLocal.Mochila:EncontrarPrimeiroFilho(xx)
	se tool e game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") então
		game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
	fim
fim

module.EquipWeapon = function()
	Se Settings["Weapon Type"] == nil ou Settings["Weapon Type"] == "" então
		Configurações["Tipo de Arma"] = "Corpo a Corpo"
	fim
	ferramenta local = jogo.Jogadores.JogadorLocal.Mochila:EncontrarPrimeiroFilho(módulo.ObterArmaAtual())
	se tool e game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") então
		game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
	fim
fim

module.FireRemotes = function(...)
    return CommF_:InvokeServer(...)
fim

module.EnableBuso = function()
	se não game.Players.LocalPlayer.Character:GetAttribute("BusoEnabled", true) então
		module.FireRemotes("Buso")
	fim
fim

module.IsAlive = function(character)
    retornar caractere e não caractere:FindFirstChild("VehicleSeat") e caractere:FindFirstChild("Humanoid") e caractere.Humanoid.Health > 0 e caractere:FindFirstChild("HumanoidRootPart")
fim

module.DetectAnyPlayersInCFrame = function(a)
    para _, v em pares(workspace.Characters:GetChildren()) faça
        se module.IsAlive(v) e v.Name ~= plr.Name e (v.HumanoidRootPart.Position - a).Magnitude <= 1000 então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

module.isnetworkowner2 = function(p1)
    local A = gethiddenproperty(plr, "SimulationRadius")
    local B = plr.Character ou Wait(plr.CharacterAdded)
    local C = game.WaitForChild(B, "HumanoidRootPart", 300)
    Se C então
        Se p1.Anchored então
            retornar falso
        fim
        se
            game.IsDescendantOf(p1, B) ou
                (C.Position - p1.Position).Magnitude <= A e module.DetectAnyPlayersInCFrame(p1.Position)
         então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

se não for o proprietário da rede, então
    isnetworkowner = function(part)
        Se module.isnetworkowner2(part) então
            return module.isnetworkowner2(part)
        fim
        retornar part.ReceiveAge == 0 e module.DetectAnyPlayersInCFrame(part.Position)
    fim
outro
    print("Você atualmente executa o suporte isnetworkowner")
fim

module.BringEnemies = function(mmb)
	sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
	local TargetPos = mmb.HumanoidRootPart.CFrame
	para _,v em próximo, WS.Enemies:GetChildren() faça
		se v.Name == mmb.Name e module.IsAlive(v) então
			se isnetworkowner(v.HumanoidRootPart) e module.GetDistance(v.HumanoidRootPart.Position) <= 500 então
                para i,a em pares(v:GetChildren()) faça
                    Se a:IsA("BasePart") então
                        a.CanCollide = false
                    fim
                fim
                se não v.HumanoidRootPart:FindFirstChild('Lock') então
                    local Lock = Instance.new('BodyVelocity')
                    Lock.Name = "Lock"
                    Lock.Parent = v.HumanoidRootPart
                    Lock.Velocity = Vector3.new(0,0,0)
                    Lock.MaxForce = Vector3.new(10000, 10000, 10000)
                fim
                v.Humanoid.WalkSpeed ​​= 0
                v:SetPrimaryPartCFrame(TargetPos)
			fim
		fim
	fim
fim

local blacklistquest = {
    "MarineQuest",
    "BartiloQuest",
    "CitizenQuest",
    "Estagiários"
}

module.CheckSea = function(b)
    Se game.PlaceId == 2753915549 e b == 1 então
        retornar verdadeiro
    senão se game.PlaceId == 4442272183 e b == 2 então
        retornar verdadeiro
    senão se game.PlaceId == 7449423635 e b == 3 então
        retornar verdadeiro
    fim
    retornar falso
fim

module.GetQuests = function()
    nível local = plr.Data.Level.Value
    Nível local Req = 0
    local mmb = {}
    Se nível >= 1 e nível < 10 então
        mmb["Mob"] = "Bandido"
        mmb["NameQuest"] = "BanditQuest1"
        mmb["ID"] = 1
        mmb["LevelReq"] = 1
    senão se lvl >= 700 e module.CheckSea(1) então
        mmb["Mob"] = "Capitão da Galera"
        mmb["NameQuest"] = "FountainQuest"
        mmb["ID"] = 2
        mmb["LevelReq"] = 700
    senão se lvl >= 1500 e module.CheckSea(2) então
        mmb["Mob"] = "Lutador de Água"
        mmb["NameQuest"] = "ForgottenQuest"
        mmb["ID"] = 2
        mmb["LevelReq"] = 1450
    outro
        para r, v em pares(Missões) faça
            para id, v1 em pares(v) faça
                local LvReq = v1.LevelReq
                para nguoi, tinh em pares (v1.Task) faça
                    se lvl >= LvReq e LevelReq <= LvReq e v1.Task[nguoi] > 1 e não table.find(blacklistquest, r) então
                        LevelReq = LvReq
                        mmb["Mob"] = nguoi
                        mmb["NameQuest"] = r
                        mmb["ID"] = id
                        mmb["LevelReq"] = LvReq
                    fim
                fim
            fim
        fim
    fim
    retornar mmb
fim

module.GetQuestBoss = function()
    cc = {}
    min = 0
    se plr.Data.Level.Value >= 700 e module.CheckSea(1) então
        cc["Nome"] = "Ciborgue"
        cc["NameQuest"] = "FountainQuest2"
        cc["ID"] = 3
    senão se plr.Data.Level.Value >= 1500 e module.CheckSea(2) então
        cc["Nome"] = "Guardião das Marés"
        cc["NameQuest"] = "ForgottenQuest"
        cc["ID"] = 3
    outro
        para r,v em seguida, Missões fazem
            para _, v1 em próximo, v faça
                para n, nn em próximo, v1.Tarefa faça
                    se plr.Data.Level.Value >= v1.LevelReq e v1.LevelReq >= min e v1.Task[n] == 1 e não table.find(blacklistquest, r) então
                        min = v1.LevelReq
                        cc["Nome"] = n
                        cc["NameQuest"] = r
                        cc["ID"] = _
                    fim
                fim
            fim
        fim
    fim
    retornar cc
fim

module.GetQuestPoint = function()
    para r, v em pares(GuideModule["Data"]["NPCList"]) faça
        se v["NPCName"] == GuideModule["Data"]["LastClosestNPC"] então
            return r["CFrame"]
        fim
    fim
fim

repita task.wait() até module.GetQuestPoint()

module.CheckDataQuest = function()
	para i, v em pares(GuideModule.Data) faça
		se i == "QuestData" então
			retornar verdadeiro
		fim
	fim
	retornar falso
fim

module.GetDataQuest = function()
    local a
	Se module.CheckDataQuest() então
		para r, v em pares(GuideModule.Data.QuestData.Task) faça
			a = r
		fim
	fim
    retornar um
fim

module.TBMobDobleQuest = function()
    local tb = {}
	para r, v em pares(Missões) faça
        para a, v1 em pares(v) faça
            para aa, lol em pares(v1.Tarefa) faça
                se aa == module.GetQuests()["Mob"] então
                    para namequest, nguvailon em pares(v) faça
                        se nguvailon.LevelReq <= game.Players.LocalPlayer.Data.Level.Value e nguvailon["Name"] ~= "Town Raid" então
                            para namemob, valores em pares(nguvailon.Task) faça
                                se os valores forem maiores que 1 então
                                    table.insert(tb, namemob)
                                fim
                            fim
                        fim
                    fim
                fim
            fim                         
        fim
    fim
    retornar tb
fim

module.GetDoubleQuest = function()
    local cc = {}
    Se Settings["Double Quest"] e module.CheckDataQuest() e module.GetDataQuest() e module.GetDataQuest() == module.GetQuests()["Mob"] e #module.TBMobDobleQuest() >= 2 então
        para r, v em pares(Missões) faça
            para a, v1 em pares(v) faça
                para aa, lol em pares(v1.Tarefa) faça
                    se aa == module.GetQuests()["Mob"] então
                        para id, nguvailon em pares(v) faça
                            para namemob, valores em pares(nguvailon.Task) faça
                                se namemob ~= module.GetQuests()["Mob"] e valores > 4 então
                                    cc["Mob"] = nomemob
                                    cc["NameQuest"] = r
                                    cc["ID"] = id
                                fim
                            fim
                        fim
                    fim
                fim
            fim
        fim
    outro
        cc["Mob"] = module.GetQuests()["Mob"]
        cc["NameQuest"] = module.GetQuests()["NameQuest"]
        cc["ID"] = module.GetQuests()["ID"]    
    fim
    retornar cc
fim

local ZinnerStorage = Instance.new("Pasta")
ZinnerStorage.Name = "ZinnerStorage"
ZinnerStorage.Parent = espaço de trabalho
repita task.wait() até workspace:FindFirstChild("ZinnerStorage")
local MobSpawning = Instance.new("Pasta")
MobSpawning.Name = "MobSpawning"
MobSpawning.Parent = ZinnerStorage
repita task.wait() até que workspace.ZinnerStorage:FindFirstChild("MobSpawning")

module.RemoveLv = function(v)
    retornar tostring(v):gsub(" %pNível. %d+%p", ""):gsub(" %pChefe de Raide%p", ""):gsub(" %pChefe%p", "")
fim

module.VerifyEnemiesSpawnPart = function()
    Negro = {}
    para _, v em pares(workspace["_WorldOrigin"].EnemySpawns:GetChildren()) faça
        v.Name = module.RemoveLv(v.Name)
        table.insert(Nigger, v)
    fim
    Hehe = {}
    para r, v em pares(Missões) faça
        para n, nn em pares(v) faça
            para _, v em pares(nn.Tarefa) faça
                se nn.Task[_] > 1 então
                    table.insert(Hehe, _)
                fim
            fim
        fim
    fim
    para r, v em pares(ReplicatedStorage:GetChildren()) faça
        se table.find(Hehe, v.Name) então
            table.insert(Nigger, v)
        fim
    fim
    para r, v em pares(WS.Enemies:GetChildren()) faça
        se table.find(Hehe, v.Name) então
            table.insert(Nigger, v)
        fim
    fim
    para _, v em pares(getnilistances()) faça
        se table.find(Hehe, v.Name) então
            table.insert(Nigger, v)
        fim
    fim
    retornar Nigger
fim

module.InsertMobSpawnPart = function()
    Mm = module.VerifyEnemiesSpawnPart()
    para _,v em pares(Mm) faça
        Se v:IsA("Parte") então
            local ole = v:Clone()
            ole.Parent = workspace.ZinnerStorage.MobSpawning
        senão se v:IsA("Model") e módulo.IsAlive(v) então
            local ole = Instance.new("Parte")
            ole.Parent = workspace.ZinnerStorage.MobSpawning
            ole.Name = module.RemoveLv(v.Name)
            ole.CFrame = v.HumanoidRootPart.CFrame
            ole.Transparency = 1
            ole.Anchored = true
            ole.CanCollide = false
            ole.CanTouch = false
        fim
    fim
fim

module.TweenSeaBoss = function(v)
    local waterbase = WS.Map["WaterBase-Plane"]
    local Seabeast = v.HumanoidRootPart
    Se (Vector3.new(0, waterbase.Position.Y, 0) - Vector3.new(0, Seabeast.Position.Y, 0)).Magnitude <= 175 então
        module.Tweento(Seabeast.CFrame * CFrame.new(0, 300, 0))
    outro
        module.Tweento(CFrame.new(Seabeast.Position.X, waterbase.Position.Y + 200, Seabeast.Position.Z))
    fim
fim

module.TweenLeviathan = function(v)
    local waterbase = WS.Map["WaterBase-Plane"]
    Leviatã local = v.HumanoidRootPart
    Se (Vector3.new(0, waterbase.Position.Y, 0) - Vector3.new(0, Leviathan.Position.Y, 0)).Magnitude <= 175 então
        module.Tweento(Leviathan.CFrame * CFrame.new(0, 30, 0))
    outro
        module.Tweento(CFrame.new(Leviathan.Position.X, waterbase.Position.Y + 70, Leviathan.Position.Z))
    fim
fim

module.CheckSeaBeast = function()
    para _,v em próximo, workspace.SeaBeasts:GetChildren() faça
        se string.find(v.Name,"SeaBeast") e module.GetDistance(v.HumanoidRootPart.Position) <= 2500 então
            Se v.Health.Value > 0 então
                retornar v
            fim
        fim
    fim
fim

module.GetShipEnemies = function()
    Navio local = {
        "PirateBasic",
        "Brigada Pirata"
    }
    Se Settings["Auto Ghost Ship"] então table.insert(Ship, "FishBoat") table.insert(Ship, "PirateGrandBrigade") fim
    para _,v em próximo, WS.Enemies:GetChildren() faça
        se v e v.Parent e table.find(Ship, v.Name) e v:FindFirstChild("Health") e v.Health.Value > 0 e module.GetDistance(v.Engine.Position) <= 2500 então
            retornar v
        fim
    fim
fim

module.VerifyEnemies = function(sech, munchit, distância)
    local tar, max = nulo, math.huge
	para i,v em próximo, WS.Enemies:GetChildren() faça
		if ((type(sech) == "table" e table.find(sech, v.Name)) ou (type(sech) == "string" e v.Name == sech)) e module.IsAlive(v) então
			se module.GetDistance(v.HumanoidRootPart.Position) <= max e module.GetDistance(v.HumanoidRootPart.Position) <= (distance or math.huge) então
				max = module.GetDistance(v.HumanoidRootPart.Position)
				tar = v
			fim
		fim
	fim
	se munchit então
        para i,v em next, ReplicatedStorage:GetChildren() faça
            if ((type(sech) == "table" e table.find(sech, v.Name)) ou (type(sech) == "string" e v.Name == sech)) e module.IsAlive(v) então
                se module.GetDistance(v.HumanoidRootPart.Position) <= max e module.GetDistance(v.HumanoidRootPart.Position) <= (distance or math.huge) então
                    max = module.GetDistance(v.HumanoidRootPart.Position)
                    tar = v
                fim
            fim
        fim
    fim
    retornar tar
fim

module.InsertMobSpawnPart()
module.CheckEyes = function()
    alleyes = {}
    para _,v em próximo, workspace.Map.TikiOutpost:WaitForChild("IslandModel"):GetChildren() faça
        se string.find(v.Name, "Eye") então
            se v.Transparência == 0 então
                table.insert(alleyes, v)
            fim
        fim
    fim
    retornar alleys
fim

module.CheckDoorPlates = function()
    return workspace.Map.Jungle.QuestPlates.Door.CanCollide
fim

module.GetPlates = function()
    para r, v em pares(WS.Map.Jungle.QuestPlates:GetChildren()) faça
        Se v:FindFirstChild("Button") então
            Se v.Button:FindFirstChild("TouchInterest") então
                retornar v.Button.CFrame
            fim
        fim
    fim
fim

module.SaberDoorOpened = function()
    return WS.Map.Jungle.Final.Part.CanCollide
fim

module.CheckDesertdDoor = function()
    return WS.Map.Desert.Burn.Fire.CanCollide
fim

module._ItemCache = nil
module._ItemCacheTime = 0
module.GetItemInventory = function()
    local agora = tick()
    se module._ItemCache e agora - module._ItemCacheTime < 0.2 então
        retornar module._ItemCache
    fim
    se não module._ItemRep então
        module._ItemRep = require(ReplicatedStorage:WaitForChild("ItemReplicationService"))
    fim
    se não module._ItemC então
        module._ItemC = require(ReplicatedStorage:WaitForChild("ItemConfig"))
    fim
    se não module._CombatU então
        module._CombatU = require(ReplicatedStorage:WaitForChild("Modules"):WaitForChild("CombatUtil"))
    fim
    local UserCache = module._ItemRep._UserCache[plr.UserId]
    se não for UserCache então
        return {}
    fim
    local Q = UserCache:GetItems("Quantidade") ou {}
    local M = UserCache:GetItems("Mastery") ou {}
    mas local = {}
    para _, v em seguida, M faça
        mas[v.ItemId] = v.Value
    fim
    local ItemList = {}
    para _, v em seguida, Q faça
        ID local = v.ItemId
        local ty, dn = "?", ""
        pcall(function()
            local c = module._ItemC.match(id):unwrap()
            se c e c.Index então
                ty = c.Index.IdType
                dn = c.Index.DebugLabel
            fim
        fim)
        entrada local = {
            Id = id,
            Nome = dn:gsub(" %[.-%]", ""),
            RawName = dn,
            Tipo = ty,
            Contagem = v.Valor,
            Domínio = mas[id],
        }
        local ok, wd = pcall(module._CombatU.GetWeaponData, module._CombatU, entry.Name)
        se estiver tudo bem e então
            entry.WeaponType = tostring(wd.WeaponType)
        fim
        tabela.inserir(ListaDeItens, entrada)
    fim
    module._ItemCache = ItemList
    module._ItemCacheTime = agora
    retornar Lista de Itens
fim

module.GetInventoryItems = function(Name)
    para _, v em próximo, módulo.GetItemInventory() faça
        se v.Name == Name então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

module.VerifyTool = function(tool)
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Mochila:ObterFilhos() faça
		se tostring(v) == ferramenta ou v.Name == ferramenta então
			retornar v
		fim
	fim
	para i, v em próximo, jogo.Jogadores.JogadorLocal.Personagem:ObterFilhos() faça
		se tostring(v) == ferramenta ou v.Name == ferramenta então
			retornar v
		fim
	fim
fim

module.TeleportWorld = function(v)
    se v == 1 e não module.CheckSea(1) então
        return module.FireRemotes("TravelMain")
    senão se v == 2 e não module.CheckSea(2) então
        return module.FireRemotes("TravelDressrosa")
    senão se v == 3 e não module.CheckSea(3) então
        return module.FireRemotes("TravelZou")
    outro
        retornar nulo
    fim
fim

module.HopServers = function(counts)
    se counts == nil então
        contagens = 10
    fim
    função local nigga(v)
        se v.Name == "ErrorPrompt" então
            Se v.Visível então
                Se v.TitleFrame.ErrorTitle.Text == "Falha no Teletransporte" então
                    v.Visible = false
                fim
            fim
            v:GetPropertyChangedSignal("Visible"):Connect(
                função()
                    Se v.Visível então
                        Se v.TitleFrame.ErrorTitle.Text == "Falha no Teletransporte" então
                            v.Visible = false
                        fim
                    fim
                fim
            )
        fim
    fim
    spawn(function()
        Fluent:Notify({ Title = "Script Hop", Content = "Hop Server In 5 Seconds", Duration = 4 })
        wait(5)
        Fluent:Notify({ Title = "Script Hop", Content = "Já disponível para o servidor Hop", Duration = 4 })
    fim)
    para i, v em próximo, jogo.CoreGui.RobloxPromptGui.promptOverlay:GetChildren() faça
        negro(v)
    fim
    game.CoreGui.RobloxPromptGui.promptOverlay.ChildAdded:Connect(nigga)
    game:GetService("Players").LocalPlayer.PlayerGui.ServerBrowser.Frame.Filters.SearchRegion.TextBox.Text = "Singapura"
    while wait() do
        para r = 1, math.huge faça
            para k, v em próximo, game.ReplicatedStorage.__ServerBrowser:InvokeServer(r) faça
                se k ~= game.JobId e v["Count"] <= counts então
                    Fluent:Notify({ Title = "Script Hop", Content = "Join Servers : " .. k, Duration = 4 })
                    game.ReplicatedStorage.__ServerBrowser:InvokeServer("teleport", k)
                fim
            fim
        fim
    fim
fim

module.RollBones = function()
    módulo.DispararRemotos("Ossos", "Comprar", 1, 1)
fim

module.GetClientElapsed = function(startTime)
    local elapsedTime = tick() - startTime
    horas locais = math.floor(tempo decorrido / 3600)
    minutos locais = math.floor((tempo decorrido % 3600) / 60)
    segundos locais = tempo decorrido % 60
    retornar string.format("%d Horas %d Minutos %d Segundos", horas, minutos, segundos)
fim

id local = {"rbxassetid://123254569317198"}
module.Dodgemobs = function(character)
    se module.IsAlive(character) e module.GetDistance(character.HumanoidRootPart.Position) <= 500 então
        Se character.Humanoid:FindFirstChildOfClass("Animator") então
            para _,v em próximo, personagem.Humanoid:FindFirstChildOfClass("Animator"):GetPlayingAnimationTracks() faça
                se table.find(id, v.Animation.AnimationId) então
                    retornar verdadeiro
                fim
            fim
        fim
    fim
    retornar falso
fim

module.CheckMaterial = function(check)
    para _, v em próximo, módulo.GetItemInventory() faça
        se v.Name == check então
            retorna v.Count ou 0
        fim
    fim
    retornar 0
fim

module.VerifyElites = function()
    para _,v em próximo, WS.Enemies:GetChildren() faça
        se table.find(module.Mobs.EliteMobs, v.Name) e module.IsAlive(v) então
            retornar v
        fim
    fim
    para _,v em próximo, ReplicatedStorage:GetChildren() faça
        se table.find(module.Mobs.EliteMobs, v.Name) e module.IsAlive(v) então
            retornar v
        fim
    fim
fim

module.VerifyMeleeMastery = function()
    melhor local = 0
    para _, v em próximo, módulo.GetItemInventory() faça
        local wt = v.WeaponType
        se v.Type == "Moveset" e wt e não wt:find("Sword") e não wt:find("Gun") e não wt:find("Blox Fruit") então
            se (v.Domínio ou 0) > melhor então
                melhor = v.Domínio
            fim
        fim
    fim
    retornar melhor
fim

module.GetDeathStepDoor = function()
    Se WS.Map.IceCastle.Hall.LibraryDoor:FindFirstChild("PhoeyuDoor") então
        return WS.Map.IceCastle.Hall.LibraryDoor.PhoeyuDoor.CanCollide
    fim
fim

module.GetRaidIslands = function(Number)
    para r, v em next, WS["_WorldOrigin"].Locations:GetChildren() faça
        Se v:IsA("Parte") então
            se string.find(v.Name, Number) então
                se module.GetDistance(v.Position) <= 2000 então
                    retornar v
                fim
            fim
        fim
    fim
fim

module.GetMobRaiding = function()
	para _,v em próximo, WS.Enemies:GetChildren() faça
		se module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 1500 então
			Se plr.PlayerGui.Main.TopHUDList.RaidTimer.Visible então
				retornar v
			fim
		fim
	fim
fim

module.CheckSwordMastery = function(xx)
    para _, v em próximo, módulo.GetItemInventory() faça
        se v.Name == xx então
            retornar v.Mastery ou 0
        fim
    fim
    retornar 0
fim

module.KillAura = function()
    para r,v em próximo, WS.Enemies:GetChildren() faça
        se v e module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 2000 então
            repita task.wait()
                v.Humanoid.Health = 0
                v.Humanoid.WalkSpeed ​​= 0
                v.Head:Destroy()
                pcall(sethiddenproperty,game.Players.LocalPlayer, "SimulationRadius", math.huge)
            até que não v ou não module.IsAlive(v)
        fim
    fim
fim

module.CheckNotify = function(aa)
    para r, v em pares(plr.PlayerGui.Notifications:GetChildren()) faça
        se v:IsA("TextLabel") e v e v.Text e string.find(string.lower(v.Text), aa) então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

module.CDKStatus = function()
    CDKProgress = {
        Mal = 0,
        Bom = 0
    }
    para r, v em próximo, CommF_:InvokeServer("CDKQuest", "Progresso", "Bom") faça
        CDKProgress[r] = v
    fim
    se CDKProgress.Evil == -2 ou CDKProgress.Evil == 4 então
        CommF_:InvokeServer("CDKQuest", "StartTrial", "Good")
    outro
        CommF_:InvokeServer("CDKQuest", "StartTrial", "Evil")
    fim
    return {CDKProgress.Evil, CDKProgress.Good}
fim

CDKQuest local
spawn(function()
    while task.wait() do
        Se Settings["Auto Dual Cursed Katana"] então
            CDKQuest = module.CDKStatus()
        fim
    fim
fim)

module.CheckMobBuso = function()
    para _,v em próximo, WS.Enemies:GetChildren() faça
        se v e module.IsAlive(v) e v:FindFirstChild("HasBuso") e module.GetDistance(v.HumanoidRootPart.Position) <= 2000 então
            retornar v
        fim
    fim
fim

module.CheckSpawn = function(aa)
    para _,v em próximo, workspace.ZinnerStorage.MobSpawning:GetChildren() faça
        se v.Name == aa então
            retornar v
        fim
    fim
fim

module.SetCameratoFirst = function()
    plr.CameraMode = Enum.CameraMode.Classic
    plr.CameraMinZoomDistance = 0.5
    plr.CameraMaxZoomDistance = 0.5
    plr.CameraMaxZoomDistance = 200
fim

module.GetHazeESP = function()
    hazemob = {}
    distância = math.huge
    nome = ""
    para _,v em próximo, plr.QuestHaze:GetChildren() faça
        Se v.Valor > 0 então
            table.insert(hazemob, v.Name)
        fim
    fim
    para _,v em seguida, hazemob faça
        Se module.CheckSpawn(v) então
            se module.GetDistance(module.CheckSpawn(v).Position) <= distance então
                distância = module.GetDistance(module.CheckSpawn(v).Position)
                nome = v
            fim
        fim
    fim
    nome de retorno
fim

module.GetHazeMobs = function()
    para _,v em próximo, espaço de trabalho.Inimigos:ObterFilhos() faça
        se v e module.IsAlive(v) e v:FindFirstChild("HazeESP") então
            retornar v
        fim
    fim
    para _,v em próximo, ReplicatedStorage:GetChildren() faça
        se v e module.IsAlive(v) e v:FindFirstChild("HazeESP") então
            retornar v
        fim
    fim
fim

module.GetBartiloPlates = function(Plates)
    para r, v em pares(WS.Map.Dressrosa.BartiloPlates:GetChildren()) faça
        se string.find(v.Name, Plates) então
            retornar v
        fim
    fim
fim

module.GetAnyMobInCFrame = function(wa)
    para _,v em próximo, WS.Enemies:GetChildren() faça
        se v e module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position, wa) <= 1000 então
            retornar v
        fim
    fim
fim

module.GetTorch = function(disname)
    disname = disname == "Yama" e "Dimensão Infernal" ou "Dimensão Celestial"
    Se WS.Map:FindFirstChild(disname) então
        nigg = WS.Map:FindFirstChild(disname)
        para i, v em pares(nigg:GetChildren()) faça
            se string.find(v.Name, "Torch") então
                se v.ProximityPrompt.Enabled == true então
                    retornar v
                fim
            fim
        fim
    fim
fim

module.DieQuest = function()
    local v = módulo.CheckMobBuso()
    se v então
        repita task.wait()
            module.Tweento(v.HumanoidRootPart.CFrame)
        até que não Settings["Auto Dual Cursed Katana"] ou não module.IsAlive(v) ou (CDKQuest[1] ~= 0 e CDKQuest[1] ~= -3)
    outro
        module.Tweento(CFrame.new(-13181.0361328125, 522.7571411132812, -6826.67041015625))
    fim
fim

module.KillHazeMobs = function()
    Se game:GetService("Lighting").LightingLayers:FindFirstChild("Haze") então
        game:GetService("Lighting").LightingLayers.Haze:Destroy()
    fim
    local Haze = module.GetHazeMobs()
    Se houver névoa, então
        Se module.IsAlive(Haze) então
            repita task.wait()
                module.EnableBuso()
                módulo.EquipWeapon()
                module.BringEnemies(Haze, true)
                module.Tweento(Haze.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
            até que não module.IsAlive(Haze) ou não Settings["Auto Dual Cursed Katana"] ou (CDKQuest[1] ~= 1 e CDKQuest[1] ~= -4)
        fim
    outro
        sexo local = módulo.GetHazeESP()
        para r,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
            se v.Name == sexo então
                repita task.wait()
                    module.Tweento(v.CFrame * CFrame.new(0, 20, 0))
                até module.GetHazeMobs() ou não Settings["Auto Dual Cursed Katana"] ou module.GetDistance(v.Position) <= 30 ou (CDKQuest[1] ~= -4 e CDKQuest[1] ~= 1)
            fim
        fim
    fim
fim

module.NoClipRocks = function()
    para _,v em next,workspace.Rocks:GetChildren() faça
        v.CanCollide = false
    fim
fim

module.QuestHellDimension = function()
    Se WS.Map:FindFirstChild("HellDimension") e WS.Map:FindFirstChild("HellDimension").Exit.BrickColor == BrickColor.new("Olivine") então
        module.Tweento(WS.Map.HellDimension.Exit.CFrame)
    fim
    Se module.GetDistance(WS._WorldOrigin.Locations["Hell Dimension"].Position) <= 2000 então
        se module.GetAnyMobInCFrame(workspace._WorldOrigin.Locations["Hell Dimension"].Position) então
            local v = module.GetAnyMobInCFrame(workspace._WorldOrigin.Locations["Hell Dimension"].Position)
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que não module.IsAlive(v) ou não Settings["Auto Dual Cursed Katana"] ou (CDKQuest[1] ~= 2 e CDKQuest[1] ~= -5)
            fim
        outro
            local Torch = module.GetTorch("Yama")
            Se for Torch, então
                print(Torch.Name)
                module.Tweento(Torch.CFrame)  
                wait(.5)
                fireproximityprompt(Torch.ProximityPrompt)
            fim
        fim
    outro
        Se module.VerifyEnemies("Soul Reaper", true) então
            local v = module.VerifyEnemies("Soul Reaper", true)
            se não module.CheckNotify("loading") e module.IsAlive(v) então
                repita task.wait()
                    module.Tweento(v.HumanoidRootPart.CFrame)
                até (CDKQuest[1] ~= 2 e CDKQuest[1] ~= -5) ou module.CheckNotify("loading") ou WS.Map:FindFirstChild("HellDimension") ou não module.IsAlive(v) ou não Settings["Auto Dual Cursed Katana"] ou module.GetDistance(workspace._WorldOrigin.Locations["Hell Dimension"].Position) <= 2000
            fim
        outro
            Se module.VerifyTool("Hallow Essence") então
                module.EquipToolName('Hallow Essence')
                module.Tweento(CFrame.new(-8932.322265625, 146.83154296875, 6062.55078125))
            outro
                módulo.RollBones()
            fim
        fim
    fim
fim

module.PedestalCheck = function()
    Pedestal local
    se CDKQuest[1] == 3 então
        Pedestal = "Pedestal2"
    senão se CDKQuest[2] == 3 então
        Pedestal = "Pedestal1"
    fim
    retornar Pedestal
fim

module.GetPirateRaid = function()
    para _,v em próximo, WS.Enemies:GetChildren() faça
        Se module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position, CFrame.new(-5546.51708984375, 313.8009948730469, -2966.331787109375).Position) <= 1000 então
            retornar v
        fim
    fim
    para _,v em próximo, ReplicatedStorage:GetChildren() faça
        Se module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position, CFrame.new(-5546.51708984375, 313.8009948730469, -2966.331787109375).Position) <= 1000 então
            retornar v
        fim
    fim
fim

module.RandomEquipWeapon = function()
	para r,v em próximo, {"Combate corpo a corpo","Espada","Arma de fogo","Fruta Blox"} faça
		module.EquipToolName(module.GetWeaponType(v))
		wait(0.2)
	fim
fim

module.GetSkill = function(type,tableskill)
    para _,v em próximo, plr.PlayerGui.Main.Skills:GetChildren() faça
        Ferramenta local = módulo.GetWeaponType(tipo)
        para r, v1 em next, v:GetChildren() faça
            se v.Name == Tool e v1.Name ~= "Template" e string.find(tableskill, v1.Name) e v1.Title.TextColor3 == Color3.fromRGB(255, 255, 255) e v1:FindFirstChild("Cooldown") e v1.Cooldown.AbsoluteSize.X < 5 então
                return {v.Name, v1.Name}
            fim
        fim
    fim
fim

module.GetBoatNPCs = function()
    maxdis = math.huge
    para _,v em seguida, os NPCs fazem
        Se v.Name == "Concessionária de Barcos de Luxo" então
            se não v:FindFirstChild("Chit") e module.GetDistance(v.HumanoidRootPart.Position) <= maxdis então
                maxdis = module.GetDistance(v.HumanoidRootPart.Position)
                retornar v
            fim
        fim
    fim
fim

module.MeetNPCBoats = function()
    local v = módulo.GetBoatNPCs()
    repita task.wait()
        se module.GetDistance(v.HumanoidRootPart.Position) > 15 então
            module.Tweento(v.HumanoidRootPart.CFrame)
        outro
            module.FireRemotes("CDKQuest","BoatQuest", WS.NPCs:FindFirstChild(v.Name))
        fim
    até (CDKQuest[2] ~= 0 e CDKQuest[2] ~= -3) ou module.GetDistance(v.HumanoidRootPart.Position) <= 10
    module.FireRemotes("CDKQuest","BoatQuest", WS.NPCs:FindFirstChild(v.Name))
    wait(0.3)
    local IntValue = Instance.new("IntValue")
    IntValue.Name = "Chit"
    IntValue.Parent = v
fim

module.PiratesRaid = function()
    Se module.GetPirateRaid() então
        local v = módulo.GetPirateRaid()
        repita task.wait()
            module.EnableBuso()
            módulo.EquipWeapon()
            module.BringEnemies(v, true)
            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
        até que não module.IsAlive(v) ou não Settings["Auto Dual Cursed Katana"] ou não module.GetPirateRaid() ou (CDKQuest[2] ~= 1 e CDKQuest[2] ~= -3)
    outro
        module.Tweento(CFrame.new(-5546.51708984375, 313.8009948730469, -2966.331787109375))
    fim
fim

module.HeavenlyDimensionQuest = function()
    Se WS.Map:FindFirstChild("HeavenlyDimension") e WS.Map:FindFirstChild("HeavenlyDimension").Exit.BrickColor == BrickColor.new("Cinza nublado") então
        module.Tweento(WS.Map.HeavenlyDimension.Exit.CFrame)
    fim			
    Se module.GetDistance(WS["_WorldOrigin"].Locations["Heavenly Dimension"].Position) <= 2000 então
        se module.GetAnyMobInCFrame(WS["_WorldOrigin"].Locations["Heavenly Dimension"].Position) então
            local v = module.GetAnyMobInCFrame(WS["_WorldOrigin"].Locations["Heavenly Dimension"].Position)
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até (CDKQuest[2] ~= 2 e CDKQuest[2] ~= -5) ou não module.IsAlive(v) ou não Settings["Auto Dual Cursed Katana"] ou WS.Map.HeavenlyDimension.Exit.BrickColor == BrickColor.new("Cinza nublado")
            fim
        outro
            tocha local = module.GetTorch("Tushita")
            Se for Torch, então
                module.Tweento(Torch.CFrame)  
                wait(.5)
                fireproximityprompt(Torch.ProximityPrompt)
            fim
        fim
    outro
        Se module.GetDistance(CFrame.new(-731.2034301757812, 381.5658874511719, -11198.4951171875).Position) > 500 então
            module.Tweento(CFrame.new(-731.2034301757812, 381.5658874511719, -11198.4951171875))
        outro
            Se module.VerifyEnemies("Cake Queen", true) e não WS.Map:FindFirstChild("HeavenlyDimension") então
                local v = module.VerifyEnemies("Cake Queen", true)
                se v e module.IsAlive(v) então
                    repita task.wait()
                        module.EnableBuso()
                        módulo.EquipWeapon()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até (CDKQuest[2] ~= 2 e CDKQuest[2] ~= -5) ou module.CheckNotify("carregando...") ou WS.Map:FindFirstChild("HeavenlyDimension") ou não module.IsAlive(v) ou não Settings["Auto Dual Cursed Katana"] ou module.GetDistance(WS["_WorldOrigin"].Locations["Heavenly Dimension"].Position) <= 2000
                fim
            senão se não module.VerifyEnemies("Cake Queen", true) e não WS.Map:FindFirstChild("HeavenlyDimension") então
                module.HopServers()
            fim
        fim
    fim
fim

module.GetMoonTexture = function()
    se module.CheckSea(1) ou module.CheckSea(2) então
        se não game:GetService("Lighting"):FindFirstChild("FantasySky") então
            retornar "http://www.roblox.com/asset/?id=9709150401"
        fim
        return game:GetService("Lighting").FantasySky.MoonTextureId
    elseif module.CheckSea(3) então
        return game:GetService("Lighting").Sky.MoonTextureId
    fim
fim

módulo.EnviarTecla = função(Tecla, Manter pressionado)
    game:GetService("VirtualInputManager"):SendKeyEvent(true,Key,false,game)
    wait((Hold or 0.1))
    game:GetService("VirtualInputManager"):SendKeyEvent(false,Key,false,game)
fim

module.CheckNearSeabeastSkill = function()

fim

module.GetMoonPhase = function()
    local MoonReturner, MoonTexture, Moon = "", module.GetMoonTexture(), {
        "http://www.roblox.com/asset/?id=9709150401",
        "http://www.roblox.com/asset/?id=9709150086",
        "http://www.roblox.com/asset/?id=9709149680",
        "http://www.roblox.com/asset/?id=9709149431",
        "http://www.roblox.com/asset/?id=9709149052",
        "http://www.roblox.com/asset/?id=9709143733",
        "http://www.roblox.com/asset/?id=9709139597",
        "http://www.roblox.com/asset/?id=9709135895"
    }
    se MoonTexture == Moon[4] então
        MoonReturner = "Lua Cheia"
    senão se MoonTexture == Moon[5] então
        MoonReturner = "Próxima Noite"
    outro
        MoonReturner = "Lua Má"
    fim
    retornar MoonReturner
fim

module.GetTime = function()
    Se game.Lighting.ClockTime < 18 e game.Lighting.ClockTime > 5 então
        retornar "Dia"
    outro
        retornar "Noite"
    fim
fim

module.ShootSoulGuitar = function(Vect)
    argumentos locais = {
        "TOQUE",
        Vetor
    }
    module.VerifyTool("Skull Guitar"):WaitForChild("RemoteEvent"):FireServer(unpack(args))    
fim

module.GetChest = function()
    distância local = math.huge
    local a
    local Chest = game:GetService("CollectionService"):GetTagged("_ChestTagged")
    para i = 1, #Baú faça
        CaliCho = (Chest[i]:GetPivot().Position - plr.Character.HumanoidRootPart.Position).Magnitude
        se Chest[i].Parent e Chest[i]:FindFirstChild("TouchInterest") e não Chest[i]:GetAttribute("IsDisabled") e CaliCho <= distância então
            distância = CaliCho
            a = Chest[i]
        fim
    fim
    retornar um
fim

module.CheckBerries = function()
    allberries = {}
    local Berries, max, returner = game:GetService("CollectionService"):GetTagged("BerryBush"), math.huge, nil
    para i = 1, #Frutas vermelhas faça
        para r, v em next, Berries[i]:GetAttributes() faça
            se table.find(module.Berries, v) então
                local a = (Berries[i].Parent:GetPivot().Position - plr.Character.HumanoidRootPart.Position).Magnitude
                se a <= max então
                    se não table.find(allberries, v) então
                        table.insert(allberries, v)
                    fim
                    max, retornador = a, Berries[i]
                fim
            fim
        fim
    fim
    return {returner, allberries}
fim

module.CheckFruitSpawn = function()
    para _,v em próximo, WS:GetChildren() faça
        se v:IsA("Model") e string.find(v.Name, "Fruit") e v.Parent e v:FindFirstChild("Handle") então
            retornar v
        fim
    fim
fim

module.CheckAndGetMastery = function(Name)
    Se module.VerifyTool(Name) então
        return module.VerifyMeleeMastery()
    fim
fim

module.ScriptClick = function()
    local VirtualInputManager = game:GetService("VirtualInputManager")
    local ViewportSize = workspace.CurrentCamera.ViewportSize
    VirtualInputManager:SendMouseButtonEvent(ViewportSize.X/2, ViewportSize.Y/2, 0, true, game, 0)
    wait()
    VirtualInputManager:SendMouseButtonEvent(ViewportSize.X/2, ViewportSize.Y/2, 0, false, game, 0)
fim

module.StoreFruits = function()
    para i, v em pares(plr.Backpack:GetChildren()) faça
        se string.find(v.Name, "Fruit") então
            argumentos locais = {
                [1] = "StoreFruit",
                [2] = v:GetAttribute("OriginalName"),
                [3] = v
            }
            game.ReplicatedStorage:FindFirstChild("Remotes"):FindFirstChild("CommF_"):InvokeServer(
                unpack(args)
            )
        fim
    fim
    para i, v em pares(plr.Character:GetChildren()) faça
        se string.find(v.Name, "Fruit") então
            argumentos locais = {
                [1] = "StoreFruit",
                [2] = v:GetAttribute("OriginalName"),
                [3] = v
            }
            game.ReplicatedStorage:FindFirstChild("Remotes"):FindFirstChild("CommF_"):InvokeServer(
                unpack(args)
            )
        fim
    fim
fim

local TableM1Fruit = {
    ["Quake-Quake"] = 1000000000,
    ["Love-Love"] = 1300000000,
	["Criação-Criação"] = 1400000000,
	["Som-Som"] = 1800000000,
    ["Buda-Buda"] = 1200000000,
    ["Spider-Spider"] = 1500000000,
    ["Phoenix-Phoenix"] = 1800000000,
    ["Portal-Portal"] = 1900000000,
    ["Rubber-Rubber"] = 2000000000,
    ["Magma-Magma"] = 2300000000,
    ["Rumble-Rumble"] = 2500000000,
    ["Blizzard-Blizzard"] = 2700000000,
    ["Gravity-Gravity"] = 3000000000,
    ["Massa-Massa"] = 3200000000,
    ["Shadow-Shadow"] = 3400000000,
    ["Venom-Venom"] = 3500000000,
    ["Control-Control"] = 3700000000,
    ["Spirit-Spirit"] = 4000000000,
    ["Dragão-Dragão"] = 4500000000,
    ["Leopard-Leopard"] = 5000000000,
	["Kitsune-Kitsune"] = 8000000000,
}

getgenv().Fruit1M = {}
local NameFruti1M = {}
para r, v em pares(TableM1Fruit) faça
    table.insert(getgenv().Fruit1M, r)
    tabela.insert(NameFruti1M, string.split(r, "-")[1] .. " Fruta")
    getgenv().Fruit1M[r] = v
fim

function module.GetFruitInBackpack()
    a = {}
    para r, v em pares(plr.Backpack:GetChildren()) faça
        para r1, v1 em pares(NameFruti1M) faça
            se v.Name == v1 e v:IsA("Tool") e não v:FindFirstChild("Data") então
                tabela.inserir(a, v.Nome)
            fim
        fim
    fim
    para r, v em pares(game.Players.LocalPlayer.Character:GetChildren()) faça
        para r1, v1 em pares(NameFruti1M) faça
            se v.Name == v1 e v:IsA("Tool") e não v:FindFirstChild("Data") então
                tabela.inserir(a, v.Nome)
            fim
        fim
    fim
    retornar um
fim

function module.DetectFruitBackpack()
    para r, v em next, plr.Backpack:GetChildren() faça
        se table.find(NameFruti1M, v.Name) e v:FindFirstChild("Handle") então
            retornar verdadeiro
        fim
    fim
    para r, v em next, plr.Character:GetChildren() faça
        se table.find(NameFruti1M, v.Name) e v:FindFirstChild("Handle") então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

function module.GetFruitInventory(tren1m)
    local max = math.huge
    gay local
    para i, v em próximo, módulo.GetItemInventory() faça
        local wt = v.WeaponType
        se v.Type == "PhysicalMoveset" ou (wt e wt:find("Blox Fruit")) então
            se tren1m == verdadeiro então
                para r1, v1 em pares(TableM1Fruit) faça
                    local base = string.split(r1, "-")[1]
                    se v.Name == r1 ou v.Name == base .. "Fruta" ou v.Name:find(base, 1, true) então
                        se tonumber(v1) < max então
                            max = tonumber(v1)
                            gay = v.Nome
                        fim
                    fim
                fim
            outro
                local encontrado = falso
                para r1, v1 em pares(TableM1Fruit) faça
                    local base = string.split(r1, "-")[1]
                    se v.Name == r1 ou v.Name == base .. "Fruta" ou v.Name:find(base, 1, true) então
                        encontrado = verdadeiro
                        quebrar
                    fim
                fim
                se não for encontrado então
                    gay = v.Nome
                fim
            fim
        fim
    fim
    retornar gay
fim

function module.StopZou()
    se plr.Data.Level.Value >= 1500 e module.CheckSea(2) então
        se CommF_:InvokeServer("BartiloQuestProgress", "Bartilo") == 3 então
            se CommF_:InvokeServer("TalkTrevor", "1") ~= 0 então
                se #module.GetFruitInBackpack() >= 1 então
                    retornar verdadeiro
                senão se não module.DetectFruitBackpack() e module.GetFruitInventory(true) então
                    retornar verdadeiro
                fim
            senão se não CommF_:InvokeServer("ZQuestProgress", "Check") então
                Se module.VerifyEnemies("Don Swan", true) então
                    retornar verdadeiro
                fim
            senão se CommF_:InvokeServer("ZQuestProgress", "Check") == 0 então
                retornar verdadeiro
            fim
        outro
            retornar falso
        fim
    fim
    retornar falso
fim

idk = ""
module.HopLow = function()
    se não sei == "" então
        decodeurl =
            game.HttpService:JSONDecode(
            game:HttpGet(
                "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100"
            )
        )
    outro
        decodeurl =
            game.HttpService:JSONDecode(
            game:HttpGet(
                "https://games.roblox.com/v1/games/" .
                    game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100&cursor=" .. sei lá
            )
        )
    fim
    se
        decodeurl.nextPageCursor e decodeurl.nextPageCursor ~= "null" e
            decodeurl.nextPageCursor ~= nil
     então
        idk = decodeurl.nextPageCursor
    fim
    para i, v em pares(decodeurl.data) faça
        se v.playing e tonumber(v.playing) <= 4 e v.id ~= game.JobId então
            game:GetService("TeleportService"):TeleportToPlaceInstance(
                game.PlaceId,
                tostring(v.id),
                plr
            )
        fim
    fim
fim

function module.CheckCakePrinceSkill()
    módulos locais = {
        A = workspace["_WorldOrigin"]:FindFirstChild("Ring"),
        B = workspace["_WorldOrigin"]:FindFirstChild("Fist")
    }
    se modules.A ou modules.B então
        Se modules.A e module.GetDistance(modules.A.Position) <= 400 então
            retornar verdadeiro
        fim
        se modules.B e module.GetDistance(modules.B.Position) <= 400 então
            retornar verdadeiro
        fim
    fim
    retornar falso
fim

module.GetDFSkills = function()
    para r,v em próximo, plr.PlayerGui.Main.Skills:GetChildren() faça
        se v.Name == (Settings["Select Mastery Type"] == "Fruit Mastery" and module.GetWeaponType("Blox Fruit") or module.GetWeaponType("Gun")) então
            para _, habilidades em pares(v:GetChildren()) faça
                se string.find(Settings["Select Skills"], skills.Name) então
                    se skills:FindFirstChild("Title") e skills.Title.TextColor3 == Color3.fromRGB(255, 255, 255) então
                        se skills:FindFirstChild("Cooldown") e skills.Cooldown.AbsoluteSize.X <= 5 então
                            retornar habilidades.Nome
                        fim
                    fim
                fim
            fim
        fim
    fim
fim

módulo.ObterIlhaPré-histórica = função ()
    Se WS.Map:FindFirstChild("PrehistoricIsland") então
        retornar verdadeiro
    outro
        retornar falso
    fim
fim

module.CheckTerrorSharkSkills = function(v)
    se module.GetDistance(v.HumanoidRootPart.Position) <= 600 então
        para _, track em pares(v.Humanoid:GetPlayingAnimationTracks()) faça
            Se track.Animation.AnimationId == "rbxassetid://14977820392" então
                retornar verdadeiro
            fim
        fim
    fim
    retornar falso
fim

module.CheckSpyStatus = function()
    se não module.CheckSea(3) então retorne "nenhum" fim
    InfoLeviathan = CommF_:InvokeServer("InfoLeviathan","1")
    Se WS["Map"]:FindFirstChild("LeviathanGate") então
        retornar "Gerador da Dimensão Congelada"
    senão se InfoLeviathan == 5 então
        "O Leviatã está à solta! Encontre-o antes que cause mais destruição."
    senão se InfoLeviathan ~= -1 então
        retornar "Comprar 1500f"
    outro
        responder "Ainda não sei de nada"
    fim
fim

module.DeleteLava = function()
    para r,v em próximo, workspace.Map.PrehistoricIsland:GetDescendants() faça
        se string.find(v.Name:lower(), "lava") então
            v:Destroy()
        fim
    fim
fim

módulo.AutoMaterial = função(nome, contagens, mobs)
    Se module.CheckMaterial(name) < counts então
        local v = módulo.VerificarInimigos(mobs)
        se v então
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v,true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que module.IsAlive(v)
            fim
        outro
            para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                se table.find(mobs, v.Name) e não module.VerifyEnemies(mobs) então
                    repita task.wait()
                        module.Tweento(v.CFrame * CFrame.new(0, 30, 0))
                    até que module.VerifyEnemies(mobs) ou module.GetDistance(v.Position) <= 10 ou module.CheckMaterial(name) >= counts
                fim
            fim
        fim
    fim
fim

module.ToPrehistoricIsland = function()
    Se module.GetPrehistoricIsland() então
        IlhaPré-histórica = WS.Map:FindFirstChild("IlhaPré-histórica")
        local Core = PrehistoricIsland e PrehistoricIsland:FindFirstChild("Core")
        local ActivationPrompt = Core e Core:FindFirstChild("ActivationPrompt")
        Se ActivationPrompt então
            module.Tweento(ActivationPrompt.CFrame)
        senão se Core e Core:FindFirstChild("PrehistoricRelic") e Core.PrehistoricRelic:FindFirstChild("Skull") então
            module.Tweento(Core.PrehistoricRelic.Skull.CFrame + Vector3.yAxis * 25)
        fim
    fim
fim

module.GetLocalBoat = function()
    para _,v em próximo, espaço de trabalho.Barcos:ObterFilhos() faça
        se v e module.GetDistance(v.VehicleSeat.Position) <= 4500 então
            se v:WaitForChild("Owner").Value == game.Players.LocalPlayer e v:FindFirstChild("Humanoid") e v.Humanoid.Value > 0 então
                retornar v
            fim
        fim
    fim
fim

module.ZoneSelected = function()
    local InfinityCFrame = Vector3.new(-99999999.21484375, 37.18704697489738464, 656.7513427734375)
    local Zone1 = Vector3.new(-21354.005859375, 37.18704697489738464, 656.7513427734375)
    local Zone2 = Vector3.new(-25180.498046875, 37.18704697489738464, 656.7513427734375)
    local Zone3 = Vector3.new(-29086.0703125, 37.18704697489738464, 656.7513427734375)
    local Zone4 = Vector3.new(-32046.49609375, 37.18704697489738464, 656.7513427734375)
    local Zone5 = Vector3.new(-36872.7265625, 37.18704697489738464, 656.7513427734375)
    local Zone6 = Vector3.new(-45061.5859375, 37.18704697489738464, 656.7513427734375)
    Se Settings["Select Zone"] == "Zone 1" ou Settings["Select Zone"] == nil então
        retornar Zona1
    senão se Settings["Selecionar Zona"] == "Zona 2" então
        retornar Zona2
    senão se Configurações["Selecionar Zona"] == "Zona 3" então
        retornar Zona3
    senão se Configurações["Selecionar Zona"] == "Zona 4" então
        retornar Zona4
    senão se Configurações["Selecionar Zona"] == "Zona 5" então
        retornar Zona5
    senão se Configurações["Selecionar Zona"] == "Zona 6" então
        retornar Zona6
    senão se Settings["Selecionar Zona"] == "Infinito" então
        print("inf")
        retornar InfinityCFrame
    fim
fim

module.GetNPCs = function(Name)
    para _,v em pares(NPCs) faça
        se v.Name == Name então
            return v:GetPivot()
        fim
    fim
fim

módulo.TweenObject = função(Objeto, Pos, Velocidade)
    Se Velocidade == nulo então
        Velocidade = 275
    fim
    Distância local = (Pos.Position - Object.Position).Magnitude
    info = TweenInfo.new(Distância / Velocidade, Enum.EasingStyle.Linear)
    tween1 =
        game:GetService("TweenService"):Create(
        Objeto,
        informação,
        {
            CFrame = Pos
        }
    )
    tween1:Play()
fim

module.GetTreeHydra = function()
    Se workspace.Map.Waterfall e workspace.Map.Waterfall.IslandModel e workspace.Map.Waterfall.IslandModel.IslandChunks e workspace.Map.Waterfall.IslandModel.IslandChunks.F então
        para r,v em pares(workspace.Map.Waterfall.IslandModel.IslandChunks.F:GetChildren()) faça
            Se v:FindFirstChild("Group") então
                Se v.Group:FindFirstChild("Part") então
                    se v.Group.Part.Color == Color3.fromRGB(130, 107, 64) ou v.Group.Part.Color == Color3.fromRGB(231, 231, 236) então
                        retornar v.Group.Part
                    fim
                fim
            fim
        fim
    fim
fim

module.NoClipBoat = function(Boolean)
    Se Booleano então
        para _, v em pares(workspace.Boats:GetDescendants()) faça
            se v:IsA("BasePart") ou v:IsA("Part") então
                v.CanCollide = false
            fim
        fim
        para r,v em próximo, plr.Character:GetDescendants() faça
            Se v:IsA("BasePart") então
                v.CanCollide = false
            fim
        fim
    outro
        para _, v em pares(workspace.Boats:GetDescendants()) faça
            se v:IsA("BasePart") ou v:IsA("Part") então
                v.CanCollide = true
            fim
        fim
    fim
fim

module.CheckMiragePuzzle = function()
    local PQ = CommF_:InvokeServer("RaceV4Progress", "Check")
    Se CommF_:InvokeServer("CheckTempleDoor") então
        retornar "Concluído"
    senão se PQ == 1 então
        retornar "Reivindicar missão NPC no castelo"
    senão se PQ == 2 então
        retornar "Pré-adolescente ao templo"
    senão se PQ == 3 então
        retornar "Continuar Missões"
    outro
        retornar "Dang gat can"
    fim
fim

module.CheckMirage = function()
    Se WS.Map:FindFirstChild("MysticIsland") então
        retornar verdadeiro
    fim
    retornar falso
fim

module.GetGear = function()
    Se workspace.Map e workspace.Map:FindFirstChild("MysticIsland") então
        para i, v em pares(WS.Map.MysticIsland:GetChildren()) faça
            se v:IsA("MeshPart") e v.MeshId == "rbxassetid://10153114969" então
                retornar v
            fim
        fim
    fim
fim

module.GetHighPart = function()
    se não module.CheckMirage então retorne fim
    para _, v em pares(WS.Map.MysticIsland:GetDescendants()) faça
        se v:IsA("MeshPart") e v.MeshId == 'rbxassetid://6105779869' então
            retornar v
        fim
    fim
fim

module.Stack = function(mode)
    se modo == "Iniciar Fazenda" então
        Se module.VerifyEnemies(module.Mobs.ripindra, true) e Settings["Auto Admin"] e module.CheckSea(3) então retorne verdadeiro
        senão se module.VerifyEnemies("Dough King", true) e Settings["Auto Dough King"] e module.CheckSea(3) então retorne verdadeiro
        senão se module.VerifyEnemies("Tyrant of the Skies", true) e Settings["Auto Tyrant of the Skies"] e module.CheckSea(3) então retorne verdadeiro
        senão se Settings["Auto Saber"] e plr.Data.Level.Value >= 200 e não module.GetInventoryItems("Saber") e (não module.SaberDoorOpened() e module.VerifyEnemies("Saber Expect", true) ou module.SaberDoorOpened()) então retorne verdadeiro
        senão se Settings["Auto Pole (1st Form)"] e plr.Data.Level.Value >= 150 e não module.GetInventoryItems("Pole (1st)") e module.VerifyEnemies("Thunder God", true) então retorne
        senão se Settings["Auto Darkbeard"] e module.VerifyEnemies("Darkbeard", true) e module.CheckSea(2) então retorne verdadeiro
        senão se Settings["Auto Elite Hunter"] e module.VerifyElites() e module.CheckSea(3) então retorne verdadeiro
        senão se Settings["Auto Yama"] e não module.GetInventoryItems("Yama") e module.CheckSea(3) e CommF_:InvokeServer("EliteHunter", "Progress") >= 30 então retorne verdadeiro
        senão se Settings["Auto Tushita"] e não module.GetInventoryItems("Tushita") e module.CheckSea(3) e (WS.Map.Turtle:FindFirstChild("TushitaGate") e module.VerifyEnemies({"rip_indra", "rip_indra True Form"}, true) ou não WS.Map.Turtle:FindFirstChild("TushitaGate")) então retorne verdadeiro
        senão se Settings["Tween to Fruit Spawn"] e module.CheckFruitSpawn() então retorne verdadeiro
        senão se Settings["Auto Travel Dressrosa"] e plr.Data.Level.Value >= 700 e CommF_:InvokeServer("DressrosaQuestProgress", "Dressrosa") ~= 0 e module.CheckSea(1) então retorne verdadeiro
        senão se Settings["Auto Bartilo"] e module.CheckSea(2) e CommF_:InvokeServer("BartiloQuestProgress", "Bartilo") ~= 3 e não module.GetInventoryItems("Warrior Helmet") e plr.Data.Level.Value >= 850 e (CommF_:InvokeServer("BartiloQuestProgress", "Bartilo") ~= 1 ou CommF_:InvokeServer("BartiloQuestProgress", "Bartilo") == 1 e module.VerifyEnemies("Jeremy", true)) então retorne verdadeiro
        fim
    fim
fim

module.SelectMaterial = function()
    local Selecionar = Configurações["Selecionar Materiais"]
    re = {}
    Se Select == "Angel Swings", então
        re["Mob"] = {"Shanda", "Royal Squad", "Royal Soldier", "Wysper", "Thunder God"}
    senão se Select == "Couro" ou Select == "Sucata Metálica" então
        re["Mob"] = (module.CheckSea(1) and {"Brute", "Pirate"} or module.CheckSea(2) and "Marine Captain" or module.CheckSea(3) and {"Jungle Pirate", "Forest Pirate"})
    senão se Select == "Minério de Magma" então
        re["Mob"] = (module.CheckSea(1) and {"Military Soldier", "Military Spy", "Magma Admiral"} or module.CheckSea(2) and {"Magma Ninja", "Lava Pirate"})
    senão se Select == "Cauda de Peixe" então
        re["Mob"] = (module.CheckSea(1) and {"Fishman Warrior", "Fishman Commando", "Fishman Lord"} or module.CheckSea(3) and {"Fishman Raider", "Fishman Captain"})
    senão se Select == "Ectoplasma" então
        re["Mob"] = {"Marinheiro", "Engenheiro de Navio", "Comissário de Bordo", "Oficial de Navio"}
    senão se Select == "Gota Mística" então
        re["Mob"] = {"Soldado do Mar","Lutador da Água"}
    senão se Select == "Material Radioativo" então
        re["Mob"] = "Equipe de Fábrica"
    senão se Select == "Presa de Vampiro" então
        re["Mob"] = "Vampiro"
    senão se Select == "Cacau Conjurado" então
        re["Mob"] = {"Batalhador de Barra de Chocolate", "Guerreiro de Cacau"}
    senão se Select == "Escama de Dragão" então
        re["Mob"] = {"Arqueiro da Tripulação do Dragão", "Guerreiro da Tripulação do Dragão"}
    senão se Select == "Pólvora" então
        re["Mob"] = "Bilionário da Pistola"
    senão se Select == "Mini Tusk" então
        re["Mob"] = "Pirata Mitológico"
    fim
    retornar re
fim

objetivo = falso
targetaim = nil

módulo.SetAimTarget = função(bool, tar)
    objetivo = booleano
    alvo = (tar ou nulo)
fim

local ListaTodosOsMateriais = {
    "Angel Swings",
    "Couro",
    "Sucata Metálica",
    "Minério de Magma",
    "Cauda de Peixe",
    "Ectoplasma",
    "Gota Mística",
    "Material Radioativo",
    "Presa de Vampiro",
    "Cacau Conjured",
    "Escama de Dragão",
    "Pólvora",
    "Mini Presa"
}

PlayerListTable = {}
local AllFeatureStorage = {}

para _,v em próximo, jogo.Jogadores:ObterJogadores() faça
    se v.Name ~= plr.Name então
        table.insert(PlayerListTable, v.Name)
    fim
fim

listaDeChefesLocais = {}
para r,v em pares(módulo.Chefes) faça
    se module.VerifyEnemies(r, true) então
        table.insert(bossesList, r)
    fim
fim

module.UpdateBoss = function()
    ListaDeChefes = {}
    para r,v em pares(módulo.Chefes) faça
        se module.VerifyEnemies(r, true) então
            table.insert(bossesList, r)
        fim
    fim
    se #bossesList == 0 então
        bossesList = {"deo co boss"}
    fim
fim

module.AutoBuso = function(v)
    spawn(function()
        enquanto Settings["Auto Buso"] e wait() faça
            module.EnableBuso()
        fim
    fim)
fim

module.AutoAwak = function(v)
    spawn(function()
        enquanto Settings["Auto Awakening V4"] e wait() faça
            se plr.Character e plr.Character:FindFirstChild("RaceTransformed") e plr.Character:FindFirstChild("RaceEnergy") e plr.Character.RaceEnergy.Value >= 1 e não plr.Character.RaceTransformed.Value então
                plr.Backpack.Awakening.RemoteFunction:InvokeServer(true)
            fim
        fim
    fim)
fim

module.AutoStats = function(v)
    spawn(function()
        enquanto Settings["Auto Stats"] e Settings["Select Stats"] ~= "" e aguarde() faça
            argumentos locais = {
                [1] = "PontoAdicionado",
                [2] = Configurações["Selecionar Estatísticas"],
                [3] = 999
            }
            CommF_:InvokeServer(unpack(args))
        fim
    fim)
fim

spawn(function()
    while wait() do
        Se LoadedHub então
            TotalChestClaimed:SetDesc(tostring(ChestCounts ou 0))
            Se Sea3 então
                MiragePuzzleStatus:SetDesc(module.CheckMiragePuzzle())
                PrehistoricStatus:SetDesc(module.GetPrehistoricIsland() and "Spawned" or "Not Spawned")
            fim
            Se Sea3 então
                CakePrinceStatus:SetDesc(module.VerifyEnemies("Cake Prince",true) and "Spawned!" or "Killed : " .. string.gsub(CommF_:InvokeServer("CakePrinceSpawner",true) or "0", "%D","") .. " Mobs")
                EliteStatus:SetDesc(module.VerifyElites() and "Spawned" or "Not spawned")
                LeviathanStatus:SetDesc(module.CheckSpyStatus())
                MirageStatus:SetDesc(module.CheckMirage() e "Gerado" ou "Não gerado")
                local berries = module.CheckBerries()[2]
                BerriesCheck:SetDesc(berries and table.concat(berries, ", ") or "not Spawned")
            outro
                CakePrinceStatus:SetDesc("Apenas o Terceiro Mar")
                EliteStatus:SetDesc("Apenas o Terceiro Mar")
                LeviathanStatus:SetDesc("Apenas o Terceiro Mar")
                MirageStatus:SetDesc("Apenas o Terceiro Mar")
                BerriesCheck:SetDesc("Apenas o Terceiro Mar")
            fim
        fim
    fim
fim)

-- ==================== CÁC HÀM TỰ ĐỘNG CHÍNH (GIỮ NGUYÊN) =====================

game:GetService("RunService").RenderStepped:Connect(function()
    se getgenv().WalkSpeed ​​e Settings["WalkSpeedToggle"] então
        plr.Character.Humanoid.WalkSpeed ​​= Settings["WalkSpeed"]
    fim
fim)

spawn(function()
    while task.wait(0) do
        Se Settings["Fast Attack"] e não MasteryOptions então
            repita task.wait() até LoadedHub ou não MasteryOptions
            pcall(FastAttack.SuperFastAttack, FastAttack)
        fim
    fim
fim)

Contagem de Peitos = 0
DojoQuestClaimed = false
DojoQuestText = ""
DragonHunterClaimed = false
DragonHunterText = ""
MasteryOptions = false
SpamSkill = false
NoClip = false
RangeOld = nulo

module.AllFuncs = {
    ["Aura de Morte"] = {function()
        para r,v em pares(workspace.Enemies:GetChildren()) faça
            Se module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 2500 então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que não seja v ou não module.IsAlive(v) ou Settings["Kill Aura"] == false
            fim
        fim
    fim, verdadeiro},
    ["Iniciar Fazenda"] = {function()
        Se module.Stack("Iniciar Fazenda") então retorne
        outro
            Se Settings["Modo Fazenda"] == "Nível" então
                Se plr.Data.Level.Value >= 50 e plr.Data.Level.Value < 150 então
                    Mobs locais = "Shanda"
                    local v = módulo.VerificarInimigos(Mobs)
                    se v e module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            módulo.TrazerInimigos(v)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até plr.Data.Level.Value >= 150 ou module.Stack("Start Farm") ou não module.IsAlive(v) ou não plr.PlayerGui.Main.Quest.Visible ou não Settings["Start Farm"]
                    senão se não v então
                        module.Tweento(CFrame.new(-7681.5751953125, 5567.17041015625, -498.3719482421875))
                    fim
                senão se plr.Data.Level.Value >= 10 e plr.Data.Level.Value < 50 então
                    Mobs locais = "Bandido do Céu"
                    local v = módulo.VerificarInimigos(Mobs)
                    se v e module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            módulo.TrazerInimigos(v)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até plr.Data.Level.Value >= 150 ou module.Stack("Start Farm") ou não module.IsAlive(v) ou não plr.PlayerGui.Main.Quest.Visible ou não Settings["Start Farm"]
                    senão se não v então
                        module.Tweento(CFrame.new(-4955.66455078125, 296.11083984375, -2900.101806640625))
                    fim
                senão se plr.Data.Level.Value < 10 ou plr.Data.Level.Value >= 150 então
                    local Boss = module.GetQuestBoss()["Name"]
                    Se module.VerifyEnemies(Boss,true) então
                        se não plr.PlayerGui.Main.Quest.Visible então
                            module.FireRemotes("StartQuest", module.GetQuestBoss()["NameQuest"], module.GetQuestBoss()["ID"])
                        outro
                            local v = module.VerifyEnemies(Boss, true)
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até module.Stack("Start Farm") ou não module.IsAlive(v) ou não plr.PlayerGui.Main.Quest.Visible ou não Settings["Start Farm"]
                        fim
                    outro
                        local QuestPoint = module.GetQuestPoint()
                        local Mob1, Mob2, Mob3 = module.GetDataQuest(), module.GetDoubleQuest()["NameQuest"], module.GetDoubleQuest()["ID"]
                        se não plr.PlayerGui.Main.Quest.Visible então
                            se module.GetDistance(QuestPoint.Position) > 10 então
                                módulo.Tweento(QuestPoint)
                            outro
                                module.FireRemotes("StartQuest", Mob2, Mob3)
                            fim
                        outro
                            local v = módulo.VerificarInimigos(Mob1)
                            se não v então
                                para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                                    se v.Name == Mob1 e não module.VerifyEnemies(Mob1) e Settings["Start Farm"] e Settings["Farm Mode"] == "Level" então
                                        repita task.wait(1)
                                            module.Tweento(v.CFrame)
                                        até que module.Stack("Start Farm") ou module.VerifyEnemies(Mob1) ou não Settings["Start Farm"] ou Settings["Farm Mode"] ~= "Level" ou module.GetDistance(v.Position) <= 10
                                    fim
                                fim
                            outro
                                repita task.wait()
                                    module.EnableBuso()
                                    módulo.EquipWeapon()
                                    módulo.TrazerInimigos(v)
                                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                até module.Stack("Start Farm") ou não module.IsAlive(v) ou não plr.PlayerGui.Main.Quest.Visible ou não Settings["Start Farm"]
                            fim
                        fim
                    fim
                fim
            senão se Settings["Modo Fazenda"] == "Bolo" e module.CheckSea(3) então
                Se module.VerifyEnemies("Cake Prince", true) então
                    local v = module.VerifyEnemies("Cake Prince", true)
                    se module.GetDistance(v.HumanoidRootPart.Position) <= 1500 então
                        Se module.IsAlive(v) então
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que module.Stack("Start Farm") ou Settings["Farm Mode"] ~= "Cake" ou não module.IsAlive(v) ou Settings["Start Farm"] == false
                        fim
                    outro
                        Se workspace.Map.CakeLoaf.BigMirror:FindFirstChild("Main") então
                            firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,workspace.Map.CakeLoaf.BigMirror.Main, 0)
                            task.wait(0.1)
                            firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,workspace.Map.CakeLoaf.BigMirror.Main, 1)
                        outro
                            module.Tweento(CFrame.new(-2124, 69, -12401))
                        fim
                    fim
                outro
                    Se module.VerifyEnemies(module.Mobs.CakeMobs, true) então
                        local v = module.VerifyEnemies(module.Mobs.CakeMobs, true)
                        Se module.IsAlive(v) então
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                módulo.TrazerInimigos(v)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que module.VerifyEnemies("Cake Prince", true) ou module.Stack("Start Farm") ou Settings["Farm Mode"] ~= "Cake" ou não module.IsAlive(v) ou Settings["Start Farm"] == false
                        fim
                    outro
                        module.Tweento(CFrame.new(-2137.133544921875, 69.97932434082031, -12324.974609375))
                    fim
                fim
            senão se Settings["Modo Fazenda"] == "Osso" e module.CheckSea(3) então
                Se module.VerifyEnemies(module.Mobs.BoneMobs, true) então
                    local v = module.VerifyEnemies(module.Mobs.BoneMobs, true)
                    Se module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            módulo.TrazerInimigos(v)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que module.Stack("Start Farm") ou Settings["Farm Mode"] ~= "Bone" ou não module.IsAlive(v) ou Settings["Start Farm"] == false
                    fim
                outro
                    module.Tweento(CFrame.new(-9496.6650390625, 172.14002990722656, 6102.12939453125))
                fim
            fim
        fim
    fim, verdadeiro},
    ["Auto Travel Dressrosa"] = {function()
        se CommF_:InvokeServer("DressrosaQuestProgress", "Dressrosa") ~= 0 então
            se plr.Data.Level.Value >= 700 e module.CheckSea(1) então
                Se workspace.Map.Ice.Door.CanCollide então
                    se não module.VerifyTool("Key") então
                        NPCKey = CFrame.new(4852.2895507813, 5.651451587677, 718.53070068359)
                        se module.GetDistance(NPCKey.Position) > 10 então
                            module.Tweento(NPCKey)
                        outro
                            module.FireRemotes("DressrosaQuestProgress", "Detective")
                        fim
                    outro
                        module.EquipToolName("Key")
                        módulo.Tweento(
                            CFrame.new(
                                1347.44092,
                                37,3843765,
                                -1322.61816,
                                0,810376644,
                                -1.14628271e-08,
                                0,585909247,
                                -4.94534582e-08,
                                1,
                                8.79637199e-08,
                                -0,585909247,
                                -1.00258987e-07,
                                0,810376644
                            )
                        )
                    fim
                outro
                    Se module.VerifyEnemies("Almirante de Gelo", verdadeiro) então
                        local v = module.VerifyEnemies("Almirante de Gelo", true)
                        repetir
                            task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que não Settings["Auto Travel Dressrosa"] ou não module.IsAlive(v)
                        module.FireRemotes("TravelDressrosa")
                    outro
                        module.Tweento(CFrame.new(1347.7124, 37.3751602, -1325.6488))
                    fim
                fim
            fim
        outro
            module.FireRemotes("TravelDressrosa")
        fim
    fim, Sea1},
    ["Auto Travel Zou"] = {função()
        task.spawn(function()
            CommF_:InvokeServer("TravelZou")
        fim)
        se plr.Data.Level.Value >= 1500 e module.CheckSea(2) então
            se CommF_:InvokeServer("BartiloQuestProgress", "Bartilo") == 3 então
                se CommF_:InvokeServer("TalkTrevor", "1") ~= 0 então
                    se #module.GetFruitInBackpack() >= 1 então
                        Se module.GetDistance(CFrame.new(-339.79840087891, 331.86065673828, 643.83178710938).Position) > 10 então
                            module.Tweento(CFrame.new(-339.79840087891, 331.86065673828, 643.83178710938))
                        outro
                            para r, v em pares(módulo.GetFruitInBackpack()) faça
                                module.EquipToolName(tostring(v))
                            fim
                            wait(0.1)
                            CommF_:InvokeServer("TalkTrevor", "1")
                            CommF_:InvokeServer("TalkTrevor", "2")
                            CommF_:InvokeServer("TalkTrevor", "3")
                        fim
                    senão se não module.DetectFruitBackpack() e module.GetFruitInventory(true) então
                        module.FireRemotes("LoadFruit", module.GetFruitInventory(true))
                    fim
                senão se não module.FireRemotes("ZQuestProgress", "Check") então
                    local v = module.VerifyEnemies("Don Swan", true)
                    se v e module.IsAlive(v) então
                        repetir
                            task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que não seja v ou não module.IsAlive(v) ou Settings["Auto Travel Zou"] == false
                    senão se não module.VerifyEnemies("Don Swan", true) então
                        module.HopServers()
                    fim
                elseif
                CommF_:InvokeServer("TalkTrevor", "1") == 0 e CommF_:InvokeServer("ZQuestProgress", "Check") == 1 e
                    CommF_:InvokeServer("ZQuestProgress", "Zou") == 0 ou CommF_:InvokeServer("ZQuestProgress").KilledIndraBoss == true
                 então
                    CommF_:InvokeServer("TravelZou")
                senão se CommF_:InvokeServer("ZQuestProgress", "Check") == 0 então
                    se module.GetDistance(workspace.Map.IndraIsland.Part.Position) > 1000 então
                        Se module.GetDistance(CFrame.new(-1926.78772, 12.1678171, 1739.80884).Position) > 10 então
                            module.Tweento(CFrame.new(-1926.78772, 12.1678171, 1739.80884))
                        outro
                            module.FireRemotes("ZQuestProgress", "Begin")
                        fim
                    outro
                        local v = module.VerifyEnemies("rip_indra")
                        se v e module.IsAlive(v) então
                            repetir
                                task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que não seja v ou não module.IsAlive(v) ou Settings["Auto Travel Zou"] == false
                            CommF_:InvokeServer("TravelZou")
                        fim
                    fim
                fim
            fim
        fim
    fim, Sea2},
    ["Domínio da Fazenda"] = {function()
        Se module.VerifyEnemies(module.Mobs.BoneMobs, true) então
            local v = module.VerifyEnemies(module.Mobs.BoneMobs, true)
            Se module.IsAlive(v) então
                local low = v.Humanoid.MaxHealth * Settings["Low Health(%)"] / 100
                repita task.wait()
                    se v.Humanoid.Health <= baixo então
                        MasteryOptions = true
                        module.EnableBuso()
                        module.BringEnemies(v, true)
                        Se Settings["Select Mastery Type"] == "Gun Mastery", então
                            module.EquipToolName(module.GetWeaponType("Gun"))
                            Se module.GetDFSkills() então
                                module.SetAimTarget(true, v.HumanoidRootPart.CFrame)
                                module.SendKey(module.GetDFSkills())
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 5))
                            outro
                                module.SetAimTarget(true, v.HumanoidRootPart.CFrame)
                                module.ScriptClick()
                                module.SetCameratoFirst()
                                workspace.CurrentCamera.CFrame = CFrame.lookAt(workspace.CurrentCamera.CFrame.Position, v.Head.Position)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 5))
                            fim
                        outro
                            module.EquipToolName(module.GetWeaponType("Blox Fruit"))
                            module.BringEnemies(v, true)
                            module.SetAimTarget(true, v.HumanoidRootPart.CFrame)
                            Se module.GetDFSkills() então
                                module.SendKey(module.GetDFSkills())
                            fim
                            workspace.CurrentCamera.CFrame = CFrame.lookAt(workspace.CurrentCamera.CFrame.Position, v.Head.Position)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 15, 0))
                        fim
                    outro
                        MasteryOptions = false
                        module.SetAimTarget(true, v.HumanoidRootPart.CFrame)
                        module.BringEnemies(v, true)
                        módulo.EquipWeapon()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    fim
                até que module.IsAlive(v) ou Settings["Farm Mastery"] seja igual a false
                MasteryOptions = false
                module.SetAimTarget(false, nil)
            fim
        outro
            module.Tweento(CFrame.new(-9496.6650390625, 172.14002990722656, 6102.12939453125))
        fim
    fim, verdadeiro},
    ["Auto Chest"] = {function()
        local v = módulo.GetChest()
        se v então
            module.Tweento(v:GetPivot())
            se module.GetDistance(v.Position) <= 10 então
                firetouchinterest(v, plr.Character.HumanoidRootPart, 0)
                firetouchinterest(v, plr.Character.HumanoidRootPart, 1)
            fim
            Se Settings["Auto Chest Hop"] então
                se ChestCounts >= tonumber(Settings["Contagem de Peitos"]) então
                    module.HopServers()
                fim
            fim
            se não v ou v:GetAttribute("IsDisabled") então
                ContagemTorácica = ContagemTorácica + 1
            fim
        fim
    fim, verdadeiro},
    ["Material Automotivo"] = {function()
        Se Settings["Select Materials"] ~= nil e Settings["Select Materials"] ~= "" então
            local Mob = module.SelectMaterial()["Mob"]
            Se module.VerifyEnemies(Mob) então
                local v = módulo.VerificarInimigos(Mob)
                Se module.IsAlive(v) então
                    repita task.wait()
                        module.EnableBuso()
                        módulo.EquipWeapon()
                        module.BringEnemies(v, true)
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até que module.IsAlive(v) ou Settings["Auto Material"]
                fim
            outro
                para r,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                    se ((typeof(Mob) == "table" e table.find(Mob, v.Name)) ou (typeof(Mob) == "string" e v.Name == Mob)) então
                        repita task.wait()
                            module.Tweento(v.CFrame * CFrame.new(0, 20, 0))
                        até que module.VerifyEnemies(module.SelectMaterial()["Mob"]) ou Settings["Auto Material"] ~= true ou module.GetDistance(v.Position) <= 30
                    fim
                fim
            fim
        fim
    fim, verdadeiro},
    ["Auto Elite Hunter"] = {function()
        Se module.VerifyElites() então
            local v = módulo.VerificarElites()
            se plr.PlayerGui.Main.Quest.Visible == false ou não string.find(plr.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, v.Name) então
                Se module.VerifyEntrance então
                    local Pos = module.GetNPCs("Caçador de Elite")
                    Se Pos e module.GetDistance(Pos.Position) > 10 então
                        módulo.Tweento(Pos)
                    elseif Pos então
                        module.FireRemotes("EliteHunter")
                    fim
                outro
                    module.FireRemotes("EliteHunter")
                fim
            senão se plr.PlayerGui.Main.Quest.Visible == true e string.find(plr.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, v.Name) então
                Se module.IsAlive(v) então
                    repita task.wait()
                        module.EnableBuso()
                        módulo.EquipWeapon()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até que não module.IsAlive(v) ou não Settings["Auto Elite Hunter"]
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Dough King"] = {function()
        Se module.VerifyEnemies("Dough King", true) então
            local v = module.VerifyEnemies("Dough King", true)
            repita task.wait()
                module.EnableBuso()
                módulo.EquipWeapon()
                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
            até que module.VerifyEnemies("Dough King", true) ou Settings["Auto Dough King"] == false
        outro
            se module.VerifyTool("Sweet Chalice") então
                Se module.VerifyEnemies(module.Mobs.CakeMobs, true) então
                    local v = module.VerifyEnemies(module.Mobs.CakeMobs, true)
                    Se module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            módulo.TrazerInimigos(v)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que não v ou não module.IsAlive(v) ou Settings["Auto Dough King"] == false ou module.VerifyEnemies("Dough King", true)
                    fim
                outro
                    module.Tweento(CFrame.new(-2137.133544921875, 69.97932434082031, -12324.974609375))
                fim
            outro
                se module.VerifyTool("Cálice de Deus") então
                    se module.CheckMaterial("Conjured Cocoa") >= 10 então
                        module.FireRemotes("SweetChaliceNpc")
                    senão se module.CheckMaterial("Conjured Cocoa") < 10 então
                        Se module.VerifyEnemies(module.Mobs.CocoaMobs, true) então
                            local v = module.VerifyEnemies(module.Mobs.CocoaMobs, true)
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                module.BringEnemies(v, true)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que module.IsAlive(v) não seja verdadeiro ou module.VerifyEnemies(module.Mobs.CocoaMobs, true) ou Settings["Auto Dough King"] == false ou module.CheckMaterial("Conjured Cocoa") >= 10
                        outro
                            para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                                se table.find(module.Mobs.CocoaMobs, v.Name) e não module.VerifyEnemies(module.Mobs.CocoaMobs) então
                                    repita task.wait()
                                        module.Tweento(v.CFrame * CFrame.new(0, 0, 0))
                                    até que module.VerifyEnemies(module.Mobs.CocoaMobs) ou não Settings["Auto Dough King"] ou module.GetDistance(v.Position) <= 10 ou module.CheckMaterial("Conjured Cocoa") >= 10
                                fim
                            fim
                        fim
                    fim
                fim
            fim
        fim
    fim, Sea3},
    ["Administração Automática"] = {função()
        se module.VerifyEnemies(module.Mobs.ripindra, true) então
            local v = module.VerifyEnemies(module.Mobs.ripindra, true)
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que module.IsAlive(v) ou Settings["Auto Admin"]
            fim
        fim
    fim, Sea3},
    ["Auto Darkbeard"] = {function()
        Se module.CheckSea(2) então
            Se module.VerifyEnemies("Darkbeard", true) então
                local v = module.VerifyEnemies("Darkbeard", true)
                Se module.IsAlive(v) então
                    repita task.wait()
                        module.EnableBuso()
                        módulo.EquipWeapon()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até que não module.IsAlive(v) ou não Settings["Auto Darkbeard"]
                fim
            outro
                se module.VerifyTool("Fist of Darkness") então
                    module.EquipToolName("Punho das Trevas")
                    module.Tweento(WS.Map.DarkbeardArena.Summoner.Detection.CFrame)
                fim
            fim
        fim
    fim,Sea2},
    ["Coleta automática de frutas vermelhas"] = {function()
        se module.CheckBerries()[1] então
            nerd = module.CheckBerries()[1]
            Se nerd:FindFirstChildOfClass("Model") então
                se module.GetDistance(nerd:FindFirstChildOfClass("Model"):GetPivot().Position) <= 15 então
                    fireproximityprompt(nerd:FindFirstChildOfClass("Model").ProximityPrompt)
                fim
                module.Tweento(nerd:FindFirstChildOfClass("Model"):GetPivot())
            outro
                module.Tweento(nerd.Parent:GetPivot())
            fim
        outro
            Se Settings["Auto Collect Berries Hop"] então
                module.HopServers()
            fim
        fim
    fim, verdadeiro},
    ["Iniciar eventos automáticos do mar"] = {function()
        Se Settings["Auto Sea Beast"] e module.CheckSeaBeast() ou (Settings["Auto Ghost Ship"] ou Settings["Auto Pirates Ship"]) e module.GetShipEnemies() ou Settings["Auto Shark and Fish Crew Member"] e module.VerifyEnemies({"Shark","Fish Crew Member"},nil,2000) ou Settings["Auto Terror Shark"] e module.VerifyEnemies("Terrorshark",nil,2000) ou Settings["Auto Piranha"] e module.VerifyEnemies("Piranha",nil,2000) então
            plr.Character.Humanoid.Sit = false
        outro
            se não module.GetLocalBoat() então
                Se module.GetDistance(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625).Position) > 50 então
                    module.Tweento(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625))
                outro
                    wait(.3)
                    módulo.DispararRemotos("ComprarBarco", (Configurações["Selecionar Barcos"] ou "Guardião"))
                fim
            outro
                Barcos = módulo.GetLocalBoat()
                Se plr.Character.Humanoid.Sit == false então
                    module.Tweento(Boats.VehicleSeat.CFrame*CFrame.new(0,2,0))
                    module.NoClipBoat(false)
                outro
                    repita wait()
                        module.NoClipBoat(true)
                        se não plr.Character.PrimaryPart:FindFirstChild("GAY") então
                            local GAY = Instance.new("BodyVelocity", plr.Character.PrimaryPart)
                            GAY.Name = "GAY"
                            GAY.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            GAY.Velocidade = módulo.ZonaSelecionada().Unidade * 260
                        fim
                        Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 24, Boats.VehicleSeat.CFrame.Z)
                    até que não Settings["Iniciar Eventos Marinhos Automáticos"] ou plr.Character.Humanoid.Sit ~= true ou Settings["Monstro Marinho Automático"] e module.CheckSeaBeast() ou (Settings["Navio Fantasma Automático"] ou Settings["Navio Pirata Automático"]) e module.GetShipEnemies() ou Settings["Tripulante Tubarão e Peixe Automático"] e module.VerifyEnemies({"Tubarão","Tripulante Peixe"},nil,2000) ou Settings["Tubarão Terrorista Automático"] e module.VerifyEnemies("Terrorshark",nil,2000) ou Settings["Piranha Automática"] e module.VerifyEnemies("Piranha",nil,2000)
                    plr.Character.HumanoidRootPart:FindFirstChild("GAY"):Destroy()
                fim
            fim
        fim
    fim, Sea3},
    ["Membro da Tripulação da Auto Shark and Fish"] = {function()
        Se module.VerifyEnemies({"Shark","Fish Crew Member"},nil,2000) então
            local v = module.VerifyEnemies({"Shark","Fish Crew Member"},nil,2000)
            se v e module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    plr.Character.Humanoid.Sit = false
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 5))
                até Settings["Auto Shark and Fish Crew Member"] ~= true ou não module.IsAlive(v)
            fim
        fim
    fim, Sea3},
    ["Auto Terror Shark"] = {function()
        Se module.VerifyEnemies("Terrorshark",nil,2000) então
            local v = module.VerifyEnemies("Terrorshark",nil,2000)
            se v e module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 2000 então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    plr.Character.Humanoid.Sit = false
                    se não module.CheckTerrorSharkSkills(v) então
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 50, 5))
                    outro
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 280, 5))
                    fim
                até Settings["Auto Terror Shark"] ~= true ou não module.IsAlive(v)
            fim
        fim
    fim, Sea3},
    ["Navio Pirata Automático"] = {function()
        Se Settings["Auto Piranha"] e module.VerifyEnemies("Piranha",nil,2000) então retorne fim
        Se não module.GetShipEnemies() então SpamSkill = falso retornar fim
        se module.GetShipEnemies() então
            local v = módulo.GetShipEnemies()
            repita task.wait()  
                se module.GetDistance(v.Engine.Position) <= 100 então
                    SpamSkill = true
                    objetivo = verdadeiro
                    alvo = CFrame.new(v.Engine.Position.X, -30, v.Engine.Position.Z)
                outro
                    SpamSkill = false
                    objetivo = falso
                fim
                plr.Character.Humanoid.Sit = false
                module.Tweento(v.Engine.CFrame*CFrame.new(0,-20,0))
            até que não seja v ou não Settings["Auto Pirates Ship"] ou v.Health.Value <= 0 ou não seja v.Parent
            objetivo = falso
            SpamSkill = false
        fim
    fim, Sea3},
    ["Auto Ghost Ship"] = {function()
        Se Settings["Auto Piranha"] e module.VerifyEnemies("Piranha",nil,2000) então retorne fim
        Se não module.GetShipEnemies() então SpamSkill = falso retornar fim
        se module.GetShipEnemies() então
            local v = módulo.GetShipEnemies()
            repita task.wait()  
                se module.GetDistance(v.Engine.Position) <= 100 então
                    SpamSkill = true
                    objetivo = verdadeiro
                    alvo = CFrame.new(v.Engine.Position.X, -30, v.Engine.Position.Z)
                outro
                    objetivo = falso
                    SpamSkill = false
                fim
                plr.Character.Humanoid.Sit = false
                module.Tweento(v.Engine.CFrame*CFrame.new(0,-20,0))
            até que não seja v ou não Settings["Auto Ghost Ship"] ou v.Health.Value <= 0 ou não seja v.Parent
            objetivo = falso
            SpamSkill = false
        fim
    fim, Sea3},
    ["Auto Sea Beast"] = {function()
        Se Settings["Auto Piranha"] e module.VerifyEnemies("Piranha",nil,2000) então retorne fim
        Se não module.CheckSeaBeast() então SpamSkill = falso retornar fim
        Se module.CheckSeaBeast() então
            local v = módulo.VerificarBestaSea()
            se v e v.Health.Value > 0 então
                repita task.wait()
                    se module.GetDistance(v.HumanoidRootPart.Position) <= 300 então
                        SpamSkill = true
                    outro
                        SpamSkill = false
                        objetivo = falso
                    fim
                    plr.Character.Humanoid.Sit = false
                    targetaim = v.HumanoidRootPart.CFrame
                    objetivo = verdadeiro
                    módulo.TweenSeaBoss(v)
                até que não seja v ou v.Health.Value <= 0 ou não Settings["Auto Sea Beast"] ou não seja v.Parent
                SpamSkill = false
                objetivo = falso
            fim
        fim
    fim, Sea3},
    ["Auto Piranha"] = {function()
        Se module.VerifyEnemies("Piranha",nil,2000) então
            local v = module.VerifyEnemies("Piranha",nil,2000)
            se v e module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 2000 então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    plr.Character.Humanoid.Sit = false
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 5))
                até Settings["Auto Piranha"] ~= true ou não module.IsAlive(v)
            fim
        fim
    fim, Sea3},
    ["Localizar Leviatã Automaticamente"] = {function()
        Se WS["Map"]:FindFirstChild("LeviathanGate") então
            Notify("Frozen Dimension Spawn",nil,nil)
            task.wait(6)
        outro
            se plr.Character.Humanoid.Sit == true então
                para _,v em próximo, espaço de trabalho.Barcos:ObterFilhos() faça
                    se v e module.GetDistance(v.VehicleSeat.Position) <= 50 então
                        Barcos locais = v
                        repita task.wait()
                        module.NoClipBoat(true)
                        se não plr.Character.PrimaryPart:FindFirstChild("GAY") então
                            local GAY = Instance.new("BodyVelocity", plr.Character.PrimaryPart)
                            GAY.Name = "GAY"
                            GAY.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            GAY.Velocidade = LeviathanHuntPos * 230
                        fim
                        se plr:GetAttribute("ExactLocation") == "" ou não plr:GetAttribute("ExactLocation") então
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 70, Boats.VehicleSeat.CFrame.Z)
                        outro
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 750, Boats.VehicleSeat.CFrame.Z)
                        fim
                        até que não Settings["Auto Find Leviathan"] ou plr.Character.Humanoid.Sit ~= true ou WS["Map"]:FindFirstChild("LeviathanGate")
                        plr.Character.HumanoidRootPart:FindFirstChild("GAY"):Destroy()
                        Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 27, Boats.VehicleSeat.CFrame.Z)
                    fim
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Leviathan"] = {function()
        se não Settings["Auto Leviathan"] ou não WS.SeaBeasts:FindFirstChild("Leviathan") então
            SpamSkill = false
            retornar
        fim
        Se WS.SeaBeasts:FindFirstChild("Leviathan") então
            Se WS.SeaBeasts:FindFirstChild("Leviathan Segment") e WS.SeaBeasts:FindFirstChild("Leviathan Segment"):FindFirstChild("Health") e WS.SeaBeasts:FindFirstChild("Leviathan Segment").Health.Value > 0 então
                local v = WS.SeaBeasts:FindFirstChild("Segmento Leviatã")
                se v e v:FindFirstChild("Saúde") e v.Saúde.Valor > 0 então
                    repita task.wait()
                        se module.GetDistance(v.HumanoidRootPart.Position) <= 100 então
                            SpamSkill = true
                            targetaim = v.HumanoidRootPart.CFrame
                            objetivo = verdadeiro
                        outro
                            objetivo = falso
                            SpamSkill = false
                        fim
                        module.EnableBuso()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 80, 0))
                    até que não seja v ou não seja v.Parent ou v.Health.Value <= 0 ou Settings["Auto Leviathan"] == false
                    objetivo = falso
                    SpamSkill = false
                fim
            outro
                local v = WS.SeaBeasts:FindFirstChild("Leviathan")
                se v e v:FindFirstChild("Saúde") e v.Saúde.Valor > 0 então
                    repita task.wait()
                        se module.GetDistance(v.HumanoidRootPart.Position) <= 100 então
                            SpamSkill = true
                            targetaim = v.HumanoidRootPart.CFrame
                            objetivo = verdadeiro
                        outro
                            SpamSkill = false
                            objetivo = falso
                        fim
                        module.EnableBuso()
                        módulo.TweenLeviathan(v)
                    até que não v ou v.Health.Value <= 0 ou Settings["Auto Leviathan"] == false ou não v.Parent ou WS.SeaBeasts:FindFirstChild("Leviathan Segment") e WS.SeaBeasts:FindFirstChild("Leviathan Segment"):FindFirstChild("Health") e WS.SeaBeasts:FindFirstChild("Leviathan Segment").Health.Value > 0
                    SpamSkill = false
                    objetivo = falso
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Sail Boat To Tiki"] = {function()
        se plr.Character.Humanoid.Sit == true então
            para _,v em próximo, espaço de trabalho.Barcos:ObterFilhos() faça
                se v e module.GetDistance(v.VehicleSeat.Position) <= 50 então
                    Barcos locais = v
                    repita task.wait()
                        module.NoClipBoat(true)
                        module.TweenObject(v.VehicleSeat, CFrame.new(-16145.2559, 27.28406239, 439.2854), 140)
                    até que não Settings["Auto Sail Boat To Tiki"] ou plr.Character.Humanoid.Sit ~= true
                    plr.Character.HumanoidRootPart:FindFirstChild("GAY"):Destroy()
                fim
            fim
        fim
    fim, Sea3},
    ["Localizar automaticamente a Ilha Kitsune"] = {function()
        Se workspace.Map:FindFirstChild("KitsuneIsland") então
            plr.Character.Humanoid.Sit = false
            module.Tweento(workspace.Map.KitsuneIsland.ShrineActive.NeonShrinePart.CFrame)
        outro
            se plr.Character.Humanoid.Sit == true então
                para _,v em próximo, espaço de trabalho.Barcos:ObterFilhos() faça
                    se v e module.GetDistance(v.VehicleSeat.Position) <= 50 então
                        Barcos locais = v
                        repita task.wait()
                        module.NoClipBoat(true)
                        se não plr.Character.PrimaryPart:FindFirstChild("GAY") então
                            local GAY = Instance.new("BodyVelocity", plr.Character.PrimaryPart)
                            GAY.Name = "GAY"
                            GAY.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            GAY.Velocidade = LeviathanHuntPos * 260
                        fim
                        se plr:GetAttribute("ExactLocation") == "" ou não plr:GetAttribute("ExactLocation") então
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 70, Boats.VehicleSeat.CFrame.Z)
                        outro
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 750, Boats.VehicleSeat.CFrame.Z)
                        fim
                        até que não Settings["Auto Find Kitsune Island"] ou plr.Character.Humanoid.Sit ~= true ou workspace.Map:FindFirstChild("KitsuneIsland")
                        Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 27, Boats.VehicleSeat.CFrame.Z)
                        NoClip = false
                    fim
                fim
            outro
                se não module.GetLocalBoat() então
                    Se module.GetDistance(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625).Position) > 50 então
                        module.Tweento(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625))
                    outro
                        wait(.3)
                        módulo.DispararRemotos("ComprarBarco", (Configurações["Selecionar Barcos"] ou "Guardião"))
                    fim
                outro
                    module.Tweento(module.GetLocalBoat().VehicleSeat.CFrame*CFrame.new(0,2,0))
                fim
            fim
        fim
    fim, Sea3},
    ["Coleta automática de membros do Azure"] = {function()
        Se WS:FindFirstChild("AttachedAzureEmber") então
            plr.Character.HumanoidRootPart.CFrame = WS:WaitForChild("EmberTemplate"):FindFirstChild("Part").CFrame
        fim
    fim, Sea3},
    ["Membro Auto Trade Azure"] = {function()
        ReplicatedStorage.Modules.Net["RF/KitsuneStatuePray"]:InvokeServer()
    fim, Sea3},
    ["Auto Awaken"] = {function()
        module.FireRemotes("Awakener","Check")
        module.FireRemotes("Awakener", "Awaken")
    fim, verdadeiro},
    ["Próximas Ilhas"] = {function()
        Se Settings["Kill Raid"] e module.GetMobRaiding() então
        outro
            Se module.GetRaidIslands("5") então
                module.Tweento(module.GetRaidIslands("5").CFrame * CFrame.new(0, 50, 0))
            elseif module.GetRaidIslands("4") então
                module.Tweento(module.GetRaidIslands("4").CFrame * CFrame.new(0, 80, 0))
            elseif module.GetRaidIslands("3") então
                module.Tweento(module.GetRaidIslands("3").CFrame * CFrame.new(0, 50, 0))
            elseif module.GetRaidIslands("2") então
                module.Tweento(module.GetRaidIslands("2").CFrame * CFrame.new(0, 50, 0))
            elseif module.GetRaidIslands("1") então
                module.Tweento(module.GetRaidIslands("1").CFrame * CFrame.new(0, 50, 0))
            fim
        fim
    fim, (Mar 2 ou Mar 3)},
    ["Iniciar Raid"] = {function()
        se module.VerifyTool("Special Microchip") então
            Se module.CheckSea(2) então
                fireclickdetector(WS.Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
            elseif module.CheckSea(3) então
                Se não workspace.Map["Boat Castle"].RaidSummon2:FindFirstChild("Button") ou não workspace.Map["Boat Castle"].RaidSummon2.Button:FindFirstChild("Main") então
                    module.Tweento(CFrame.new(-5048.35986, 314.874817, -2905.125, 0.709312141, -3.71912066e-08, 0.704894483, 3.08777999e-08, 1, 2.16900649e-08, -0.704894483, 6.38056319e-09, 0.709312141))
                outro
                    fireclickdetector(workspace.Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
                fim
            fim
        fim
    fim, (Mar 2 ou Mar 3)},
    ["Ataque de Eliminação"] = {function()
        Se module.Stack("Iniciar Fazenda") então retorne
        outro
            Se plr.PlayerGui.Main.TopHUDList.RaidTimer.Visible então
                para _,v em próximo, WS.Enemies:GetChildren() faça
                    se module.IsAlive(v) e module.GetDistance(v.HumanoidRootPart.Position) <= 1500 então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            module.BringEnemies(v, true)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até plr.PlayerGui.Main.TopHUDList.RaidTimer.Visible == false ou module.Stack("Iniciar Fazenda") ou não module.IsAlive(v) ou não Settings["Matar Raid"]
                    fim
                fim
            fim
        fim
    fim, (Mar 2 ou Mar 3)},
    ["Auto Roll Fruits"] = {function()
        module.FireRemotes("Primo", "Comprar")
    fim, verdadeiro},
    ["Tween para Germinação de Frutos"] = {function()
        Se module.CheckFruitSpawn() então
            local Fruits = module.CheckFruitSpawn()
            module.Tweento(Fruits.Handle.CFrame)
        fim
    fim, verdadeiro},
    ["Armazene Frutas"] = {function()
        Se StopStoreFruit, retorne o fim.
        módulo.StoreFruits()
    fim, verdadeiro},
    ["Auto Pole (1ª forma)"] = {function()
        se não module.GetInventoryItems("Pole (1st From)") e não module.CheckSea(1) então module.TeleportWorld(1) retorne fim
        se não module.GetInventoryItems("Pole (1st From)") e module.CheckSea(1) e plr.Data.Level.Value >= 150 então
            local v = module.VerifyEnemies("Thunder God", true)
            se v e module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que module.IsAlive(v) ou Settings["Auto Pole (1st form)"]
            outro
                Se Settings["Opções de Salto"] então
                    task.wait(.1)
                    module.HopServers()
                fim
            fim
        fim
    fim, Sea1},
    ["Auto Saber"] = {function()
        se não module.GetInventoryItems("Saber") e não module.CheckSea(1) então module.TeleportWorld(1) retorne fim
        se não module.GetInventoryItems("Saber") e plr.Data.Level.Value >= 200 então
            se module.SaberDoorOpened() então
                Se module.CheckDoorPlates() então
                    pcall(function()
                        module.Tweento(module.GetPlates())
                    fim)
                outro
                    Se module.CheckDesertdDoor() então
                        se não module.VerifyTool("Torch") então
                            local Torch = WS.Map.Jungle.Torch
                            module.Tweento(Torch.CFrame)
                        outro
                            module.EquipToolName("Tocha")
                            module.Tweento(CFrame.new(1115.25354, 4.95647621, 4349.24463, -0.624247193, 5.46374288e-08, 0.781226873, -1.33858959e-08, 1, -8.06341163e-08, -0.781226873, -6.07930417e-08, -0.624247193))
                        fim
                    outro
                        local RichsonProgess = CommF_:InvokeServer("ProQuestProgress", "RichSon")
                        Se RichsonProgess ~= 0 e RichsonProgess ~= 1 então
                            se não module.VerifyTool("Cup") então
                                se module.GetDistance(WS.Map.Desert.Cup.CFrame.Position) > 100 então
                                    module.Tweento(WS.Map.Desert.Cup.CFrame)
                                outro
                                    module.GetHRP().CFrame = WS.Map.Desert.Cup.CFrame
                                fim
                            outro
                                module.EquipToolName("Copo")
                                wait(0.4)
                                module.FireRemotes("ProQuestProgress","FillCup", module.VerifyTool("Cup"))
                                wait(0.2)
                                module.FireRemotes("ProQuestProgress","SickMan")
                            fim
                        senão se RichsonProgess == 0 então
                            Se module.VerifyEnemies("Mob Leader", true) então
                                local v = module.VerifyEnemies("Mob Leader", true)
                                se module.IsAlive(v) e v.Parent então
                                    repita task.wait()
                                        module.EnableBuso()
                                        módulo.EquipWeapon()
                                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                    até que não seja v ou não module.IsAlive(v) ou Settings["Auto Saber"] == false
                                fim
                            outro
                                module.Tweento(CFrame.new(-2836.19385, 7.92910671, 5484.93408))
                            fim
                        senão se RichsonProgess == 1 então
                            se não module.VerifyTool("Relic") então
                                local Rich = CFrame.new(-908.814819, 14.1188612, 4077.24658)
                                Se module.GetDistance(Rich.Position) > 10 então
                                    módulo.Tweento(Rich)
                                outro
                                    module.FireRemotes("ProQuestProgress","RichSon")
                                fim
                            outro
                                module.EquipToolName("Relic")
                                module.Tweento(CFrame.new(-1404.43835, 29.8870087, 4.62949038, 0.883046508, 9.38910727e-09, 0.469285458, -2.02383887e-08, 1, 1.80749922e-08, -0.469285458, -2.54586396e-08, 0.883046508))
                            fim
                        fim
                    fim
                fim
            outro
                Se module.VerifyEnemies("Saber Expert", true) então
                    local v = module.VerifyEnemies("Saber Expert", true)
                    repita task.wait()
                        module.EnableBuso()
                        módulo.EquipWeapon()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até que module.IsAlive(v) não seja verdadeiro ou v.Parent não seja verdadeiro ou Settings["Auto Saber"] seja falso
                outro
                    Se Settings["Opções de Salto"] então
                        task.wait(.1)
                        module.HopServers()
                    fim
                fim
            fim
        fim
    fim, Sea1},
    ["Rengoku automático"] = {função()
        se não module.GetInventoryItems("Rengoku") e não module.CheckSea(2) então module.TeleportWorld(2) retorne fim
        Se module.GetInventoryItems("Rengoku") então retorne fim
        se não module.GetInventoryItems("Rengoku") então
            se não module.VerifyTool("Hidden Key") então
                Se module.VerifyEnemies("Almirante de Gelo Desperto", verdadeiro) então
                    local v = module.VerifyEnemies("Almirante de Gelo Desperto", true)
                    Se module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que não module.IsAlive(v) ou não Settings["Auto Rengoku"] ​​ou module.VerifyTool("Hidden Key")
                    fim
                senão se não Settings["Opções de Salto"] então
                    Mobs local = módulo.Mobs.RengokuMobs
                    Se module.VerifyEnemies(Mobs) então
                        local v = módulo.VerificarInimigos(Mobs)
                        Se module.IsAlive(v) então
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                module.BringEnemies(v, true)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que não module.IsAlive(v) ou não Settings["Auto Rengoku"] ​​ou module.VerifyTool("Hidden Key")
                        fim
                    outro
                        para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                            se table.find(Mobs, v.Name) então
                                repita task.wait()
                                    module.Tweento(v.CFrame * CFrame.new(0, 20, 0))
                                até que module.GetDistance(v.Position) <= 30 ou module.VerifyEnemies(Mobs) ou não Settings["Auto Rengoku"] ​​ou module.VerifyTool("Hidden Key")
                            fim
                        fim
                    fim
                senão se Configurações["Opções de Salto"] então
                    task.wait(.1)
                    module.HopServers()
                fim
            outro
                module.EquipToolName("Tecla Oculta")
                module.Tweento(CFrame.new(6571.1201171875, 299.23028564453, -6967.841796875))
            fim
        fim
    fim, Sea2},
    ["Auto Yama"] = {function()
        Se module.GetInventoryItems("Yama") então
        outro
            se CommF_:InvokeServer("EliteHunter", "Progress") >= 30 então
                se não WS.Map.Waterfall:FindFirstChild("SealedKatana") então
                    module.Tweento(CFrame.new(5250.71924, 19.842907, 453.177002))
                outro
                    se module.GetDistance(WS.Map.Waterfall.SealedKatana.Hitbox.Position) <= 10 então
                        fireclickdetector(WS.Map.Waterfall.SealedKatana.Hitbox.ClickDetector)
                    outro
                        module.Tweento(WS.Map.Waterfall.SealedKatana.Hitbox.CFrame)
                    fim
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Tushita"] = {função()
        Se module.GetInventoryItems("Tushita") então
        outro
            local TushitaProgress = CommF_:InvokeServer("TushitaProgress")
            se não TushitaProgress.OpenedDoor então
                Se module.VerifyEnemies({"rip_indra", "rip_indra True Form"}, true) então
                    se não module.VerifyTool("Holy Torch") então
                        módulo.Tweento(
                            CFrame.new(
                                5717.06592,
                                18.8161335,
                                252.124573,
                                0,926925123,
                                -3.25000045e-08,
                                -0,375246346
                                3.45466091e-08,
                                1,
                                -1.2735254e-09,
                                0,375246346,
                                -1.17830261e-08,
                                0,926925123
                            )
                        )
                    outro
                        module.EquipToolName("Tocha Sagrada")
                        para r = 1, 5 faça
                            module.FireRemotes("TushitaProgress", "Torch", r)
                        fim
                    fim
                fim
            outro
                local v = module.VerifyEnemies("Longma", true)
                se v e module.IsAlive(v) então
                    repetir
                        task.wait()
                        módulo.EquipWeapon()
                        module.EnableBuso()
                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                    até que não module.IsAlive(v) ou não v.Parent
                senão se não v então
                    module.HopServers()
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Hallow Scythe"] = {function()
        se não module.CheckSea(3) ou module.GetInventoryItems("Hallow Scythe") então retorne fim
        local SR = module.VerifyEnemies("Soul Reaper", true)
        se SR então
            Se module.IsAlive(SR) então
                v local = SR
                repita task.wait()
                    módulo.EquipWeapon()
                    module.EnableBuso()
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que não module.IsAlive(SR) ou não module.VerifyEnemies("Soul Reaper", true) ou não Settings["Auto Hallow Scythe"]
            fim
        outro
            Se module.VerifyTool("Hallow Essence") então
            module.EquipToolName('Hallow Essence')
            module.Tweento(CFrame.new(-8932.322265625, 146.83154296875, 6062.55078125))
            outro
                módulo.RollBones()
            fim
        fim
    fim, Sea3},
    ["Auto Dual Cursed Katana"] = {function()
        Se module.CheckSwordMastery("Yama") >= 350 e module.CheckSwordMastery("Tushita") >= 350 então
            Se workspace.Map.Turtle.Cursed:FindFirstChild("Breakable") então
                Se module.GetDistance(CFrame.new(-12130.51171875, 577.8272705078125, -6707.11474609375).Position) <= 10 então
                    module.FireRemotes("CDKQuest", "DoorNpc")
                    module.FireRemotes("CDKQuest", "OpenDoor", true)
                    Se WS.Map.Turtle.Cursed:FindFirstChild("Breakable") então
                        WS.Map.Turtle.Cursed.Breakable:Destroy()
                    fim
                outro
                    module.Tweento(CFrame.new(-12130.51171875, 577.8272705078125, -6707.11474609375))
                fim
                retornar
            fim
            se CDKQuest[1] == 4 e CDKQuest[2] == 4 então
                Se workspace.Map.Turtle.Cursed.Pedestal1.ProximityPrompt.Enabled então
                    se module.GetDistance(workspace.Map.Turtle.Cursed.Pedestal1.Position) > 10 então
                        module.Tweento(workspace.Map.Turtle.Cursed.Pedestal1.CFrame)
                    outro
                        fireproximityprompt(WS.Map.Turtle.Cursed.Pedestal1.ProximityPrompt)
                    fim
                outro
                    Se module.GetDistance(WS.Map.Turtle.Cursed.Pedestal3.Position) > 10 e WS.Map.Turtle.Cursed.PlacedGem.Transparency ~= 0 então
                        module.Tweento(WS.Map.Turtle.Cursed.Pedestal3.CFrame)
                    fim
                    se WS.Map.Turtle.Cursed.PlacedGem.Transparency == 0 então
                        se não module.VerifyEnemies("Cursed Skeleton Boss", true) então
                            module.Tweento(CFrame.new(-12341.66796875, 603.3455810546875, -6550.6064453125))
                        outro
                            local v = module.VerifyEnemies("Chefe Esqueleto Amaldiçoado", true)
                            se v e module.IsAlive(v) então
                                repita task.wait()
                                    module.EnableBuso()
                                    módulo.EquipWeapon()
                                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                até que module.IsAlive(v) ou Settings["Auto Dual Cursed Katana"]
                            fim
                        fim
                    outro
                        se module.GetDistance(WS.Map.Turtle.Cursed.Pedestal3.Position) < 10 então
                            fireproximityprompt(WS.Map.Turtle.Cursed.Pedestal3.ProximityPrompt)
                            wait(2)
                        fim
                    fim
                fim
            fim
            se module.PedestalCheck() ~= nil então
                local Pedestal = module.PedestalCheck()
                se module.GetDistance(WS.Map.Turtle.Cursed[Pedestal].Position) <= 10 então
                    fireproximityprompt(WS.Map.Turtle.Cursed[Pedestal].ProximityPrompt)
                outro
                    module.Tweento(WS.Map.Turtle.Cursed[Pedestal].CFrame)
                fim
            fim
            se CDKQuest[1] ~= -2 e CDKQuest[1] ~= 4 então
                se CDKQuest[1] == 0 ou CDKQuest[1] == -3 então
                    módulo.DieQuest()
                senão se CDKQuest[1] == 1 ou CDKQuest[1] == -4 então
                    módulo.KillHazeMobs()
                senão se CDKQuest[1] == 2 ou CDKQuest[1] == -5 então
                    módulo.QuestHellDimension()
                fim
            outro
                se CDKQuest[2] == 0 ou CDKQuest[2] == -3 então
                    module.MeetNPCBoats()
                senão se CDKQuest[2] == 1 ou CDKQuest[2] == -4 então
                    module.PiratesRaid()
                senão se CDKQuest[2] == 2 ou CDKQuest[2] == -5 então
                    módulo.HeavenlyDimensionQuest()
                fim
            fim
        outro
            itens locais = (module.CheckSwordMastery("Yama") < 350 e "Yama" ou module.CheckSwordMastery("Tushita") < 350 e "Tushita" ou "nenhum")
            Fluent:Notify({ Title = "Auto CDK", Content = items .. " < 350 Mastery", Duration = 4 })
            module.FireRemotes("LoadItem", items)
            wait(5)
        fim
    fim, Sea3},
    ["Auto Superhuman"] = {function()
        se CommF_:InvokeServer("BuySuperhuman",true) ~= 1 então
            se não Settings["Black Legs"] então
                se module.VerifyTool("Black Leg") então
                    se module.VerifyMeleeMastery() >= 300 então
                        Configurações["Pernas Pretas"] = verdadeiro
                        module.Save()
                    fim
                outro
                    module.FireRemotes("BuyBlackLeg")
                fim
            senão se não Settings["Electro"] então
                Se module.VerifyTool("Electro") então
                    se module.VerifyMeleeMastery() >= 300 então
                        Configurações["Electro"] = true
                        module.Save()
                    fim
                outro
                    module.FireRemotes("BuyElectro")
                fim
            senão se não Settings["Fishman Karate"] então
                se module.VerifyTool("Fishman Karate") então
                    se module.VerifyMeleeMastery() >= 300 então
                        Configurações["Caratê Homem-Peixe"] = verdadeiro
                        module.Save()
                    fim
                outro
                    module.FireRemotes("BuyFishmanKarate")
                fim
            senão se não Settings["Garra de Dragão"] então
                se module.VerifyTool("Black Leg") então
                    se module.VerifyMeleeMastery() >= 300 então
                        Configurações["Garra de Dragão"] = verdadeiro
                        module.Save()
                    fim
                outro
                    module.FireRemotes("BlackbeardReward", "DragonClaw", "1")
                    module.FireRemotes("BlackbeardReward", "DragonClaw", "2")
                fim
            outro
                module.FireRemotes("BuySuperhuman",true)
                module.FireRemotes("BuySuperhuman")
            fim
        outro
            module.FireRemotes("BuySuperhuman",true)
            module.FireRemotes("BuySuperhuman")
        fim
    fim, verdadeiro},
    ["Passo de Morte Automática"] = {function()
        se CommF_:InvokeServer("BuyDeathStep", true) ~= 1 então
            se module.VerifyTool("Black Leg") então
                se module.VerifyMeleeMastery() >= 400 então
                    Se module.GetDeathStepDoor() então
                        se não module.VerifyTool("Chave da Biblioteca") então
                            local v = module.VerifyEnemies("Almirante de Gelo Desperto", true)
                            se v e module.IsAlive(v) então
                                repita task.wait()
                                    module.EnableBuso()
                                    módulo.EquipWeapon()
                                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                até que não module.IsAlive(v) ou não Settings["Auto Death Step"] ou module.VerifyTool("Library Key")
                            senão se não v então
                                Se Settings["Opções de Salto"] então
                                    module.HopServers()
                                fim
                            fim
                        outro
                            module.EquipToolName("Chave da Biblioteca")
                            module.Tweento(CFrame.new(6375.9126, 296.634583, -6843.14062, -0.849467814, 1.5493983e-08, -0.527640462, 3.70608895e-08, 1, -3.0301031e-08, 0.527640462, -4.5294577e-08, -0.849467814))
                        fim
                    outro
                        module.FireRemotes("BuyDeathStep")
                    fim
                fim
            outro
                module.FireRemotes("BuyBlackLeg")
            fim
        outro
            module.FireRemotes("BuyDeathStep")
        fim
    fim, verdadeiro},
    ["Auto Sharkman Karate"] = {function()
        se não module.CheckSea(2) e CommF_:InvokeServer("BuySharkmanKarate",true) ~= 1 então retorne module.TeleportWorld(2) fim
        se CommF_:InvokeServer("BuySharkmanKarate",true) ~= 1 então
            se module.VerifyTool("Fishman Karate") então
                se module.VerifyMeleeMastery() >= 400 então
                    if CommF_:InvokeServer("BuySharkmanKarate",true) == "Perdi as chaves de casa, você poderia me ajudar a encontrá-las? Obrigado." então
                        se não module.VerifyTool("Water Key") então
                            se module.VerifyEnemies("Tide Keeper",true) então
                                local v = module.VerifyEnemies("Tide Keeper",true)
                                Se module.IsAlive(v) então
                                    repita task.wait()
                                        module.EnableBuso()
                                        módulo.EquipWeapon()
                                        module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                    até que não module.IsAlive(v) ou não Settings["Auto Sharkman Karate"] ou module.VerifyTool("Water Key")
                                fim
                            outro
                                Se Settings["Opções de Salto"] então
                                    module.HopServers()
                                fim
                            fim
                        outro
                            module.FireRemotes("BuySharkmanKarate",true)
                        fim
                    outro
                        module.FireRemotes("BuySharkmanKarate")
                    fim
                fim
            outro
                module.FireRemotes("BuyFishmanKarate")
            fim
        outro
            module.FireRemotes("BuySharkmanKarate")
        fim
    fim, verdadeiro},
    ["Garra Elétrica Automática"] = {função()
        se CommF_:InvokeServer("BuyElectricClaw",true) ~= 1 então
            Se module.VerifyTool("Electro") então
                se module.VerifyMeleeMastery() >= 400 então
                    se não CommF_:InvokeServer("BuyElectricClaw", "Start") então
                        Se module.GetDistance(CFrame.new(-10369.0390625, 331.6894836425781, -10133.06640625)) > 10 então
                            module.Tweento(CFrame.new(-10369.0390625, 331.6894836425781, -10133.06640625))
                        outro
                            module.FireRemotes("BuyElectricClaw", "Start")
                            wait(.5)
                        fim
                    senão se CommF_:InvokeServer("BuyElectricClaw", "Start") == 4 então
                        module.Tweento(CFrame.new(-12549.7236, 337.511505, -7470.36328))
                    outro
                        module.FireRemotes("BuyElectricClaw")
                    fim
                fim
            outro
                module.FireRemotes("BuyElectro")
            fim
        outro
            module.FireRemotes("BuyElectricClaw")
        fim
    fim, Sea3},
    ["Auto Dragon Talon"] = {function()
        se CommF_:InvokeServer("BuyDragonTalon",true) ~= 1 então
            Se CommF_:InvokeServer("BuyDragonTalon",true) == "Acenda sua chama." então
                se module.VerifyTool("Garra de Dragão") então
                    se module.VerifyMeleeMastery() >= 400 então
                        se não module.VerifyTool("Essência de Fogo") então
                            módulo.RollBones()
                        outro
                            module.FireRemotes("BuyDragonTalon",true)
                        fim
                    fim
                outro
                    module.FireRemotes("BlackbeardReward", "DragonClaw", "1")
                    module.FireRemotes("BlackbeardReward", "DragonClaw", "2")
                fim
            outro
                module.FireRemotes("BuyDragonTalon")
            fim
        outro
            module.FireRemotes("BuyDragonTalon")
        fim
    fim, Sea3},
    ["Auto Godhuman"] = {function()
        se CommF_:InvokeServer("BuyGodhuman",true) ~= 1 então
            MateriaisNecessários = {
                ["Cauda de Peixe"] = 20,
                ["Minério de Magma"] = 20,
                ["Escama de Dragão"] = 10,
                ["Gota Mística"] = 10
            }
            se não Settings["SuperhumanOkay"] então
                se module.VerifyTool("Superhuman") e module.VerifyMeleeMastery() >= 400 então
                    Configurações["SuperhumanOkay"] = true
                    module.Save()
                senão se não module.VerifyTool("Superhuman") então
                    module.FireRemotes("BuySuperhuman")
                fim
            senão se não Settings["DeathStepOkay"] então
                se module.VerifyTool("Death Step") e module.VerifyMeleeMastery() >= 400 então
                    Configurações["DeathStepOkay"] = true
                    module.Save()
                senão se não module.VerifyTool("Death Step") então
                    module.FireRemotes("BuyDeathStep")
                fim
            senão se não Settings["ElectricClawOkay"] então
                se module.VerifyTool("Electric Claw") e module.VerifyMeleeMastery() >= 400 então
                    Configurações["ElectricClawOkay"] = true
                    module.Save()
                senão se não module.VerifyTool("Garra Elétrica") então
                    module.FireRemotes("BuyElectricClaw")
                fim
            senão se não Settings["SharkmanOkay"] então
                Se module.VerifyTool("Sharkman Karate") e module.VerifyMeleeMastery() >= 400 então
                    Configurações["SharkmanOkay"] = true
                    module.Save()
                senão se não module.VerifyTool("Sharkman Karate") então
                    module.FireRemotes("BuySharkmanKarate")
                fim
            senão se não Settings["DragonTalonOkay"] então
                se module.VerifyTool("Dragon Talon") e module.VerifyMeleeMastery() >= 400 então
                    Configurações["DragonTalonOkay"] = true
                    module.Save()
                senão se não module.VerifyTool("Dragon Talon") então
                    module.FireRemotes("BuyDragonTalon")
                fim
            outro
                local MateriaisSuficientes = verdadeiro
                para nome, contagens em seguida, MateriaisNecessários faça
                    Se module.CheckMaterial(name) < counts então
                        MateriaisSuficientes = falso
                        se nome == "Escama de Dragão" então
                            se não module.CheckSea(3) então module.TeleportWorld(3) fim
                            lista de mobs local = {
                                "Arqueiro da Tripulação do Dragão",
                                "Guerreiro da Tripulação do Dragão"
                            }
                            module.AutoMaterial(name, counts, MobsList)
                        senão se nome == "Cauda de Peixe" então
                            se não module.CheckSea(3) então module.TeleportWorld(3) fim
                            lista de mobs local = {
                                "Invasor Homem-Peixe",
                                "Capitão Homem-Peixe"
                            }
                            module.AutoMaterial(name, counts, MobsList)
                        senão se nome == "Gota Mística" então
                            se não module.CheckSea(2) então module.TeleportWorld(2) fim
                            lista de mobs local = {
                                "Soldado do Mar",
                                "Lutador de Água"
                            }
                            module.AutoMaterial(name, counts, MobsList)
                        senão se nome == "Minério de Magma" então
                            se não module.CheckSea(1) então module.TeleportWorld(1) fim
                            lista de mobs local = {
                                "Soldado Militar",
                                "Espião Militar"
                            }
                            module.AutoMaterial(name, counts, MobsList)
                        fim
                    fim
                fim
                Se houver materiais suficientes, então
                    module.FireRemotes("BuyGodhuman",true)
                    module.FireRemotes("BuyGodhuman")
                fim
            fim
        outro
            CommF_:InvokeServer("BuyGodhuman",true)
            module.FireRemotes("BuyGodhuman")
        fim
    fim, verdadeiro},
    ["Auto Soul Guitar"] = {function()

    fim, Sea3},
    ["Surpresas Aleatórias"] = {function()
        módulo.RollBones()
    fim,Mar3},
    ["Haki de Observação de Alcance Infinito"] = {
        função()
            se RangeOld == nulo então
                RangeOld = game:GetService("Players").LocalPlayer.VisionRadius.Value
            fim
            game:GetService("Players").LocalPlayer.VisionRadius.Value = math.huge
        fim,
        verdadeiro
    },
    ["Localização automática de ilha pré-histórica"] = {function()
        Se module.GetPrehistoricIsland() então
            se plr.Character.Humanoid.Sit == true então
                plr.Character.Humanoid.Sit = false
            fim
            module.ToPrehistoricIsland()
        outro
            se plr.Character.Humanoid.Sit == true então
                para _,v em próximo, espaço de trabalho.Barcos:ObterFilhos() faça
                    se v e module.GetDistance(v.VehicleSeat.Position) <= 50 então
                        Barcos locais = v
                        repita task.wait()
                        module.NoClipBoat(true)
                        se não plr.Character.PrimaryPart:FindFirstChild("GAY") então
                            local GAY = Instance.new("BodyVelocity", plr.Character.PrimaryPart)
                            GAY.Name = "GAY"
                            GAY.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            GAY.Velocidade = LeviathanHuntPos * 260
                        fim
                        se plr:GetAttribute("ExactLocation") == "" ou não plr:GetAttribute("ExactLocation") então
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 70, Boats.VehicleSeat.CFrame.Z)
                        outro
                            Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 750, Boats.VehicleSeat.CFrame.Z)
                        fim
                        até que não Settings["Auto Find Prehistoric Island"] ou plr.Character.Humanoid.Sit ~= true ou module.GetPrehistoricIsland()
                        plr.Character.HumanoidRootPart:FindFirstChild("GAY"):Destroy()
                        Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 27, Boats.VehicleSeat.CFrame.Z)
                    fim
                fim
            outro
                se não module.GetLocalBoat() então
                    Se module.GetDistance(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625).Position) > 50 então
                        module.Tweento(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625))
                    outro
                        wait(.3)
                        módulo.DispararRemotos("ComprarBarco", (Configurações["Selecionar Barcos"] ou "Guardião"))
                    fim
                outro
                    module.Tweento(module.GetLocalBoat().VehicleSeat.CFrame*CFrame.new(0,2,0))
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Ilha Pré-histórica"] = {function()
        se não module.GetPrehistoricIsland() então SpamSkill = falso retornar fim
        Se module.VerifyEnemies("Lava Golem") e Settings["Auto Lava Golem"] então retorne fim
        Se module.GetPrehistoricIsland() então
            se plr.Character.Humanoid.Sit == true então
                plr.Character.Humanoid.Sit = false
            fim
            Ilha local = WS.Map:FindFirstChild("IlhaPré-histórica")
            se plr.PlayerGui.Main.TopHUDList.RaidTimer.Visible e Island.Core:FindFirstChild("VolcanoRocks") então
                task.spawn(module.KillAura)
                module.DeleteLava()
                Se Island:FindFirstChild("InteriorLava") então
                    Island:FindFirstChild("InteriorLava"):Destroy()
                fim
                se plr.PlayerGui.Main.TopHUDList.RaidTimer.Visible e Island.Core:FindFirstChild("VolcanoRocks") então
                    para r,v em próximo, Island.Core.VolcanoRocks:GetChildren() faça
                        se v:IsA("Model") e v.Name == "Rock" então
                            Se v:FindFirstChild("volcanorock") então
                                se v:FindFirstChild("VFXLayer") e v.VFXLayer.At1Beam.Enabled então
                                    repita task.wait()
                                        se module.GetDistance(v.volcanorock.Position) <= 100 então
                                            SpamSkill = true
                                        outro
                                            SpamSkill = false
                                            objetivo = falso
                                        fim
                                        module.Tweento(v.volcanorock.CFrame)
                                    até que v.VFXLayer.At1Beam.Enabled não esteja ativado ou Island não esteja definido ou Settings["Auto Prehistoric Island"] == false
                                    SpamSkill = false
                                senão se v:FindFirstChild("VFXLayer") e não v.VFXLayer.At1Beam.Enabled então
                                    Se Core e Core:FindFirstChild("PrehistoricRelic") e Core.PrehistoricRelic:FindFirstChild("Skull") então
                                        module.Tweento(Core.PrehistoricRelic.Skull.CFrame + Vector3.yAxis * 25)
                                    fim
                                fim
                            fim
                        fim
                    fim
                fim
            outro
                local Core = Island:FindFirstChild("Core")
                local ActivationPrompt = Core e Core:FindFirstChild("ActivationPrompt")
                Se ActivationPrompt então
                    se module.GetDistance(ActivationPrompt.Position) > 10 então
                        module.Tweento(ActivationPrompt.CFrame)
                    outro
                        fireproximityprompt(ActivationPrompt.ProximityPrompt)
                    fim
                senão se Core e Core:FindFirstChild("PrehistoricRelic") e Core.PrehistoricRelic:FindFirstChild("Skull") então
                    module.Tweento(Core.PrehistoricRelic.Skull.CFrame + Vector3.yAxis * 25)
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Lava Golem"] = {function()
        se module.VerifyEnemies("Lava Golem") então
            local v = module.VerifyEnemies("Lava Golem")
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que module.IsAlive(v) ou Settings["Auto Lava Golem"]
            fim
        fim
    fim, Sea3},
    ["Coleta Automática de Ovos de Dragão"] = {function()
        Se module.GetPrehistoricIsland() então
            Se workspace.Map.PrehistoricIsland.Core:FindFirstChild("SpawnedDragonEggs") e workspace.Map.PrehistoricIsland.Core.SpawnedDragonEggs:FindFirstChild("DragonEgg") então
                local egg = workspace.Map.PrehistoricIsland.Core.SpawnedDragonEggs:FindFirstChild("DragonEgg")
                se module.GetDistance(egg:GetPivot().Position) <= 10 então
                    fireproximityprompt(egg.Molten.ProximityPrompt)
                outro
                    module.Tweento(egg:GetPivot())
                fim
            fim
        fim
    fim, Sea3},
    ["Habilidades de Aimbot"] = {function()
        para r,v em próximo, WS.Characters:GetChildren() faça
            se v.Name == (getgenv().TargetSelect ou "") então
                se v e v.Parent e v.Humanoid.Health > 0 então
                    repita task.wait()
                        module.SetAimTarget(true, v.HumanoidRootPart.CFrame)
                    até que não v ou não v.Parent ou v.Humanoid.Health <= 0 ou não Settings["Aimbot Skills"]
                    module.SetAimTarget(false, nil)
                fim
            fim
        fim
    fim, verdadeiro},
    ["Compra automática de Haki Spawn"] = {function()
        module.FireRemotes("ColorsDealer","2")
    fim, Sea3},
    ["Compra automática de espada lendária"] = {function()
        module.FireRemotes("LegendarySwordDealer", "2")
    fim, Sea3},
    ["Auto Tirano dos céus"] = {function()
        se não module.CheckSea(3) então retorne fim
        Se Settings["Start Farm"] e não module.VerifyEnemies("Tyrant of the Skies", true) então retorne fim
        local v = module.VerifyEnemies("Tyrant of the Skies", true)
        se v então
            Se module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até Settings["Auto Tyrant of the skies"] ~= true ou não module.IsAlive(v) ou não v.Parent
            fim
        senão se #module.CheckEyes() >= 4 então
            spawn(function()
                module.Tweento(CFrame.new(-16217.470703125, 155.212158203125, 1389.8223876953125))
            fim)
            Fluent:Notify({ Title = "Notificação de Script", Content = "Por favor, destrua toda a cerâmica", Duration = 10 })
            wait(11)
        outro
            local v = module.VerifyEnemies(module.Mobs.TikiMobs)
            se v então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que Settings["Auto Tyrant of the skies"] ~= true ou não module.IsAlive(v) ou #module.CheckEyes() >= 4
            outro
                para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                    se table.find(module.Mobs.TikiMobs, v.Name) e não module.VerifyEnemies(module.Mobs.TikiMobs) então
                        repita task.wait()
                            module.Tweento(v.CFrame * CFrame.new(0, 0, 0))
                        até que module.VerifyEnemies(module.Mobs.TikiMobs) ou não Settings["Auto Tyrant of the skies"] ou module.GetDistance(v.Position) <= 10
                    fim
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Collect Dino Bone"] = {function()
        para r,v em próximo, espaço de trabalho:ObterFilhos() faça
            se v:IsA("MeshPart") e v.Name == "DinoBone" então
                repita task.wait()
                    module.Tweento(v.CFrame)
                até que não esteja em Configurações["Coleta Automática de Ossos de Dinossauro"] ou não esteja em v ou não esteja em v.Pai
            fim
        fim
    fim, Sea3},
    ["Teletransportar para Jogadores"] = {function()
        Se getgenv().SelectPlayers ~= "" e getgenv().SelectPlayers ~= nil então
            Jogador local = getgenv().SelecionarJogadores
            Se workspace.Characters[Player] então
                module.Tweento(workspace.Characters[Player].HumanoidRootPart.CFrame)
            fim
        fim
    fim,verdadeiro},
    ["Auto Farming 600 Maestria Todas as Espadas"] = {function()
        local nowtool = module.GetWeaponType("Sword")
        Se module.VerifyTool(nowtool) então
            local Mastery = module.VerifyTool(nowtool).Level.Value
            Se Maestria >= 600 então
                para r, v em próximo, módulo.GetItemInventory() faça
                    se v.WeaponType e v.WeaponType:find("Sword") então
                        se (v.Domínio ou 0) < 600 então
                            module.FireRemotes("LoadItem", v.Name)
                        fim
                    fim
                fim
            fim
        fim
    fim,verdadeiro},
    ["Alavanca de acionamento automático"] = {function()
        local Progress = module.CheckMiragePuzzle()
        Se Progresso == "Concluído", então
            Notificar("Alavanca de Puxar Concluída",nil,7)
            task.wait(8)
            retornar
        fim
        Se Progresso == "Reivindicar missão do NPC no castelo", então
            Se module.GetDistance(CFrame.new(-5356.1416015625, 313.75048828125, -2491.4521484375)) <= 10 então
                module.FireRemotes("RaceV4Progress", "Begin")
            outro
                module.Tweento(CFrame.new(-5356.1416015625, 313.75048828125, -2491.4521484375))
            fim
        senão se Progresso == "Entre o templo" então
            Se module.GetDistance(CFrame.new(3029.850830078125, 2281.01025390625, -7325.95556640625)) <= 10 então
                module.FireRemotes("RaceV4Progress", "Teleport")
            outro
                module.Tweento(CFrame.new(3029.850830078125, 2281.01025390625, -7325.95556640625))
            fim
        senão se Progresso == "Continuar Missões" então
            module.FireRemotes("RaceV4Progress", "Continue")
        outro
            se Progresso ~= "Concluído" e module.CheckMirage() então
                local HighPos = CFrame.new(0,0,0)
                Se module.GetHighPart() então
                    HighPos = module.GetHighPart().CFrame * CFrame.new(0, 12, 0)
                outro
                    HighPos = WS.Map.MysticIsland.WorldPivot * CFrame.new(0, 500, 0)
                fim
                Se module.GetGear() então
                    local Gear = module.GetGear()
                    Se Gear.Transparency == 0 e Gear.CanCollide não, então
                        repita task.wait()
                            module.Tweento(Gear.CFrame)
                        até que não Gear ou Settings["Auto Pull Lever"] == false
                    senão se Gear e Gear.Transparency ~= 0 então
                        se module.GetDistance(HighPos.Position) <= 10 então
                            Se module.GetTime() == "Noite" então
                                repita task.wait()
                                    module.SetCameratoFirst()
                                    WS.CurrentCamera.CFrame = CFrame.lookAt(WS.CurrentCamera.CFrame.Position, game:GetService("Lighting"):GetMoonDirection() + WS.CurrentCamera.CFrame.Position)
                                    module.SendKey("T")
                                até que Gear e Gear.Transparency == 0 e Gear.CanCollide == false ou não Settings["Auto Pull Lever"]
                            outro
                                module.Tweento(HighPos)
                            fim
                        outro
                            module.Tweento(HighPos)
                        fim
                    fim
                outro
                    module.Tweento(HighPos)
                fim
            fim
        fim
    fim, Sea3},
    ["Auto Soul Reaper"] = {function()
        local SR = module.VerifyEnemies("Soul Reaper", true)
        se SR então
            Se module.IsAlive(SR) então
                v local = SR
                repita task.wait()
                    módulo.EquipWeapon()
                    module.EnableBuso()
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que não module.IsAlive(SR) ou não module.VerifyEnemies("Soul Reaper", true) ou não Settings["Auto Soul Reaper"]
            fim
        outro
            Se module.VerifyTool("Hallow Essence") então
            module.EquipToolName('Hallow Essence')
            module.Tweento(CFrame.new(-8932.322265625, 146.83154296875, 6062.55078125))
            outro
                módulo.RollBones()
            fim
        fim
    fim, Sea3},
    ["Auto Blaze Embers"] = {function()
        Se não module.CheckNotify("tarefa concluída") então SpamSkill = falso module.SetAimTarget(falso) fim
        se não WS:FindFirstChild("EmberTemplate") então
            se não DragonHunterClaimed então
                local Pos = CFrame.new(5863.29150390625, 1209.4527587890625, 809.9525756835938)
                se module.GetDistance(Pos) <= 10 então
                    local Progress = game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("Net"):WaitForChild("RF/DragonHunter"):InvokeServer({Context = "Check"})
                    se typeof(Progress) ~= "boolean" então
                        se não Progresso["Texto"] então
                            Net:WaitForChild("RF/DragonHunter"):InvokeServer({Context = "RequestQuest"})
                        outro
                            DragonHunterClaimed = true
                            DragonHunterText = Progress["Text"]
                        fim
                    fim
                outro
                    módulo.Tweento(Pos)
                fim
            outro
                se DragonHunterText ~= "" então
                    Se DragonHunterText == "Destrua 10 árvores na Ilha Hydra." então
                        Se module.GetTreeHydra() então
                            local Trees = module.GetTreeHydra()
                            repita task.wait()
                                se module.GetDistance(Trees.Position) <= 100 então
                                    SpamSkill = true
                                    module.SetAimTarget(true, Trees.CFrame)
                                outro
                                    SpamSkill = false
                                    module.SetAimTarget(false)
                                fim
                                module.Tweento(Trees.CFrame)
                            até que não seja DragonHunterClaimed ou não seja Trees ou não seja Trees.Parent ou module.CheckNotify("tarefa concluída")
                            SpamSkill = false
                            module.SetAimTarget(false)
                        fim
                    elseif DragonHunterText == "Derrote 3 agressores venenosos na Ilha Hydra." então
                        Multidões locais = "Agressor Venenoso"
                        Se module.VerifyEnemies(Mobs, true) então
                            local v = module.VerifyEnemies(Mobs, true)
                            Se module.IsAlive(v) então
                                repita task.wait()
                                    module.EnableBuso()
                                    módulo.EquipWeapon()
                                    module.BringEnemies(v, true)
                                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                até que não DragonHunterClaimed ou não module.IsAlive(v) ou não Settings["Auto Blaze Embers"] ou module.CheckNotify("tarefa concluída")
                            fim
                        outro
                            para r,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                                se v.Name == Mobs então
                                    repita task.wait()
                                        module.Tweento(v.CFrame * CFrame.new(0, 20, 0))
                                    até que module.VerifyEnemies(Mobs, true) ou não Settings["Auto Blaze Embers"] ou module.GetDistance(v.Position) <= 30 ou module.CheckNotify("task completed") ou não DragonHunterClaimed
                                fim
                            fim
                        fim
                    elseif DragonHunterText == "Derrote 3 Executores da Hidra na Ilha da Hidra." então
                        Mobs locais = "Executor da Hydra"
                        Se module.VerifyEnemies(Mobs, true) então
                            local v = module.VerifyEnemies(Mobs, true)
                            Se module.IsAlive(v) então
                                repita task.wait()
                                    module.EnableBuso()
                                    módulo.EquipWeapon()
                                    module.BringEnemies(v, true)
                                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                                até que não DragonHunterClaimed ou não module.IsAlive(v) ou não Settings["Auto Blaze Embers"] ou module.CheckNotify("tarefa concluída")
                            fim
                        outro
                            para r,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                                se v.Name == Mobs então
                                    repita task.wait()
                                        module.Tweento(v.CFrame * CFrame.new(0, 20, 0))
                                    até que module.VerifyEnemies(Mobs, true) ou não Settings["Auto Blaze Embers"] ou module.GetDistance(v.Position) <= 30 ou module.CheckNotify("task completed") ou não DragonHunterClaimed
                                fim
                            fim
                        fim
                    fim
                fim
            fim
        senão se WS:FindFirstChild("EmberTemplate") e WS.EmberTemplate:FindFirstChild("Part") então
            plr.Character.PrimaryPart.CFrame = WS.EmberTemplate.Part.CFrame
        fim
    fim, Sea3},
    ["Auto Boss"] = {
        função()
            local Boss, Info = module.Getboss(Settings["Select Boss"])
            Se Boss e module.VerifyEnemies(Boss, true) então
                se Info e Info["IsBoss"] e Settings["Take Quests"] e não plr.PlayerGui.Main.Quest.Visible então
                    se module.GetDistance(Info.Quest[2]) <= 10 então
                        module.FireRemotes("StartQuest", Info.Quest[1], 3)
                    outro
                        module.Tweento(Info.Quest[2])
                    fim
                senão se não Info ou não Info["IsBoss"] ou não Settings["Take Quests"] ou plr.PlayerGui.Main.Quest.Visible então
                    local v = module.VerifyEnemies(Boss, true)
                    se v e module.IsAlive(v) então
                        repita task.wait()
                            module.EnableBuso()
                            módulo.EquipWeapon()
                            module.BringEnemies(v, true)
                            module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                        até que não module.IsAlive(v) ou não Settings["Auto Boss"]
                    fim
                fim
            fim
        fim,verdadeiro
    },
    ["Auto All Boss"] = {
        função()
            local v = module.VerifyEnemies(module.Bosses, true)
            se v e module.IsAlive(v) então
                repita task.wait()
                    module.EnableBuso()
                    módulo.EquipWeapon()
                    module.BringEnemies(v, true)
                    module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                até que module.IsAlive(v) ou Settings["Auto All Boss"]
            fim
        fim,verdadeiro
    },
    ["Auto Dojo Trainer"] = {function()
        se não DojoQuestClaimed então
            local Pos = module.GetNPCs("Dojo Trainer")
            Se Pos e module.GetDistance(Pos) <= 10 então
                local Progress = Net:WaitForChild("RF/InteractDragonQuest"):InvokeServer({NPC = "Dojo Trainer",Command = "RequestQuest"})
                se typeof(Progress) == "table" então
                    se Progresso["Missão"] então
                        para r,v em próximo, Progresso["Missão"] faça
                            DojoQuestText = Progress["Quest"]["QuestName"]
                            DojoQuestClaimed = true
                        fim
                    outro
                        print("[hoang beo] missão não reivindicada")
                    fim
                fim
            outro
                se Pos então module.Tweento(Pos) fim
            fim
        outro
            se DojoQuestText ~= "" então
                Net:WaitForChild("RF/InteractDragonQuest"):InvokeServer({NPC = "Dojo Trainer",Command = "ClaimQuest"})                
                Se DojoQuestText == "Admissão" então
                    local QuestPoint = module.GetQuestPoint()
                    local Mob1, Mob2, Mob3 = module.GetDataQuest(), module.GetDoubleQuest()["NameQuest"], module.GetDoubleQuest()["ID"]
                    se não plr.PlayerGui.Main.Quest.Visible então
                        se module.GetDistance(QuestPoint.Position) > 10 então
                            módulo.Tweento(QuestPoint)
                        outro
                            module.FireRemotes("StartQuest", Mob2, Mob3)
                        fim
                    outro
                        local v = módulo.VerificarInimigos(Mob1)
                        se não v então
                            para _,v em próximo, WS.ZinnerStorage.MobSpawning:GetChildren() faça
                                se v.Name == Mob1 e não module.VerifyEnemies(Mob1) e Settings["Auto Dojo Trainer"] então
                                    repita task.wait()
                                        module.Tweento(v.CFrame)
                                        task.wait(1)
                                    até que module.VerifyEnemies(Mob1) ou não Settings["Auto Dojo Trainer"] ou module.GetDistance(v.Position) <= 10
                                fim
                            fim
                        outro
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                módulo.TrazerInimigos(v)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que não module.IsAlive(v) ou não plr.PlayerGui.Main.Quest.Visible ou não Settings["Auto Dojo Trainer"]
                        fim
                    fim
                senão se DojoQuestText == "Guerreiro da Água" então
                    Se module.VerifyEnemies({"Shark","Piranha","Terrorshark","Fish Crew Member"}, nil, 2000) então
                        plr.Character.Humanoid.Sit = false
                        local v = module.VerifyEnemies({"Shark","Piranha","Terrorshark","Fish Crew Member"}, nil, 2000)
                        se v e module.IsAlive(v) então
                            repita task.wait()
                                module.EnableBuso()
                                módulo.EquipWeapon()
                                módulo.TrazerInimigos(v)
                                module.Tweento(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
                            até que não module.IsAlive(v) ou não Settings["Auto Dojo Trainer"] ou não DojoQuestClaimed
                        fim
                    outro
                        se não module.GetLocalBoat() então
                            Se module.GetDistance(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625).Position) > 50 então
                                module.Tweento(CFrame.new(-16214.6767578125, 9.09604263305664, 406.43853759765625))
                            outro
                                wait(.3)
                                module.FireRemotes("BuyBoat", "Guardian")
                            fim
                        outro
                            Barcos = módulo.GetLocalBoat()
                            Se plr.Character.Humanoid.Sit == false então
                                module.Tweento(Boats.VehicleSeat.CFrame*CFrame.new(0,2,0))
                                module.NoClipBoat(false)
                            outro
                                repita wait()
                                    module.NoClipBoat(true)
                                    se não plr.Character.PrimaryPart:FindFirstChild("GAY") então
                                        local GAY = Instance.new("BodyVelocity", plr.Character.PrimaryPart)
                                        GAY.Name = "GAY"
                                        GAY.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                                        GAY.Velocidade = LeviathanHuntPos * 260
                                    fim
                                    Boats.VehicleSeat.CFrame = CFrame.new(Boats.VehicleSeat.CFrame.X, 24, Boats.VehicleSeat.CFrame.Z)
                                até que não Settings["Auto Dojo Trainer"] ou plr.Character.Humanoid.Sit ~= true ou module.VerifyEnemies({"Shark","Piranha","Terrorshark","Fish Crew Member"}, nil, 2000)
                                plr.Character.HumanoidRootPart:FindFirstChild("GAY"):Destroy()
                            fim
                        fim
                    fim
                fim
            fim
        fim
    fim, Sea3}
}

spawn(function()
    while wait() do
        Se module.CheckNotify("tarefa concluída") então
            DojoQuestClaimed = false
            DragonHunterClaimed = false
        fim
    fim
fim)

spawn(function()
    while wait() do
        Se Settings["Auto Look At Moon"] então
            WS.CurrentCamera.CFrame = CFrame.lookAt(WS.CurrentCamera.CFrame.Position, game:GetService("Lighting"):GetMoonDirection() + WS.CurrentCamera.CFrame.Position)
        fim
    fim
fim)

spawn(function()
    while wait() do
        se SpamSkill então
            pcall(function()
                Se Settings["Usar Melee"] e module.GetSkill("Melee",Settings["Habilidades de Melee"]) então
                    local Skills = module.GetSkill("Melee",Settings["Melee Skills"])
                    module.EquipToolName(Skills[1])
                    module.SendKey(Skills[2])
                senão se Settings["Usar Espada"] e module.GetSkill("Espada", Settings["Habilidades de Espada"]) então
                    local Skills = module.GetSkill("Sword",Settings["Sword Skills"])
                    module.EquipToolName(Skills[1])
                    module.SendKey(Skills[2])
                senão se Settings["Usar Arma"] e module.GetSkill("Arma", Settings["Habilidades com Armas"]) então
                    local Skills = module.GetSkill("Gun",Settings["Gun Skills"])
                    module.EquipToolName(Skills[1])
                    module.SendKey(Skills[2])
                senão se Settings["Usar Blox Fruit"] e module.GetSkill("Blox Fruit", Settings["Habilidades de Blox Fruit"]) então
                    local Skills = module.GetSkill("Blox Fruit",Settings["Blox Fruit Skills"])
                    module.EquipToolName(Skills[1])
                    module.SendKey(Skills[2])
                outro
                    módulo.RandomEquipWeapon()
                fim
            fim)
        fim
    fim
fim)

spawn(function()
    while wait() do
        se mirar e alvejar então
            pcall(function()
                Câmera local = espaço de trabalho.CâmeraAtual
                local CameraPosition = Camera.CFrame.Position
                local TargetPosition = targetaim.Position
                local LookVector = (PosiçãoAlvo - PosiçãoCâmera).Unit
                local NewCFrame = CFrame.lookAt(CameraPosition, CameraPosition + LookVector)
                Camera.CFrame = NewCFrame
            fim)
        fim
    fim
fim)

module.LoadScript = function()
    task.spawn(function()
        repita task.wait() até LoadedHub
        while task.wait() do
            NoClip = false
            x, xx = pcall(function()
                para cada função nome, função em pares(módulo.TodasAsFunções) faça
                    se Settings[namefunc] e func[2] então
                        NoClip = true
                        func[1]()
                    fim
                fim
            fim)
            se não x então imprima(xx) fim
        fim
    fim)
    
    pcall(function()
        WS.Map["WaterBase-Plane"].Size = Vector3.new(1000, 113, 1000)
        se module.CheckSea(2) e workspace.Map.CircleIsland.Detail:lFindFirstChild("LavaParts") então
            workspace.Map.CircleIsland:WaitForChild("Detail"):FindFirstChild("LavaParts"):Destroy()
        fim
    fim)
fim

LoadedHub = true
module.LoadScript()
print("Carregado " .. start_script_time)
print("anh yeu em kuri")
