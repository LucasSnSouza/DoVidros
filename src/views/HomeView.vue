<template>

    <div class="home w-full h-full scroll-y bg-color-brand-two">
        
        <div 
            style="
                background-image: url('/arts/header-background.png');
                box-shadow: 0px 4px 10px #00000011;
            "
            id="home-page"
            class="home-header flex x-center y-center"
        >

            <div
                style="
                    height: 94%;
                    backdrop-filter: blur(6px);
                "
                class="home-panel rounded-xlg color-brand-two ghost"
            >
                <h1>Soluções personalizadas para suas ideias</h1>
                <p class="subtitle">Faça agora um orçamento conosco e leve mais sofisticação, luz e segurança para seu lar.</p>
                <div class="flex gap-md">
                    <ButtonBasic
                        class="bg-color-brand-two p-lg pointer rounded-md color-brand-two ghost flex gap-md y-center"
                        style="background-color: #FFFFFFBB; backdrop-filter: blur(6px);"
                        @click="openWhatsappTalk()"
                    >
                        <MiscIcon
                            icon="whatsapp"
                            class="bg-color-brand-one"
                            :size="[24,24]"
                        />
                        <p class="color-brand-one">Entre em contato</p>
                    </ButtonBasic>
                    <ButtonBasic
                        class="bg-color-brand-two p-lg pointer rounded-md color-brand-two ghost"
                        style="background-color: #FFFFFFBB; backdrop-filter: blur(6px);"
                        @click="openInstagram()"
                    >
                        <MiscIcon
                            icon="instagram"
                            class="bg-color-brand-one"
                            :size="[24,24]"
                        />
                    </ButtonBasic>
                </div>
            </div>

        </div>

        <div 
            class="other-pages flex flex-column"
        >
            <div id="about-page" class="home-about flex flex-column gap-lg p-xlg">
    
                <div class="page-header">
                    <p>Sobre nós</p>
                    <div>
                        <h1 class="font-xlg" style="line-height: 30px;">Trabalhando com excelência a mais de 10 anos</h1>
                        <h2 class="lobster">Conheça nossa jornada até aqui</h2>
                    </div>
                </div>
    
                <div class="about-frame w-full">
    
                    <p class="about-description o-half">
                        A Dó Vidros é uma empresa especializada em projetos personalizados e corporativos em vidro, oferecendo soluções modernas, seguras e sofisticadas para transformar ambientes residenciais e comerciais.
                    </p>
    
                    <div class="about-cards">
    
                        <div 
                            v-for="(item, index) in works_list"
                            class="about-card color-brand-four ghost rounded-md p-lg flex flex-column gap-md"
                            style="box-shadow: 0px 2px 8px #00000011;"
                            :index="index"
                        >
                            <div class="flex">
                                <div class="color-brand-one ghost p-sm rounded-md">
                                    <MiscIcon
                                        :icon="item.icon"
                                        class="bg-color-brand-one"
                                        :size="[24,24]"
                                    />
                                </div>
                            </div>
                            <h1 class="color-brand-one font-lg">{{ item.title }}</h1>
                            <p class="color-brand-one font-md o-half">{{ item.description }}</p>
                        </div>
    
                    </div>
    
                </div>
    
            </div>
    
            <div id="gallery-page" class="home-gallery p-xlg flex flex-column gap-xlg">
    
                <div class="page-header">
                    <p>Galeria</p>
                    <div>
                        <h1 class="font-xlg" style="line-height: 30px;">Nosso trabalho visualmente para você</h1>
                        <h2 class="lobster">Todos nossos trabalhos você encontra aqui</h2>
                    </div>
                </div>
    
                <div class="flex gap-md warp x-center">
    
                    <ButtonBasic
                        v-for="(item, index) in filtering_buttons"
                        class="bg-color-brand-four rounded-lg pointer"
                        :class="{ 'p-sm': item.selected }"
                        :index="index"
                        @click="selectFilterButtons(index), selected_filtering = item.filter"
                    >
                        <div 
                            class="sub-button bg-color-brand-two h-full flex x-center y-center rounded-lg"
                            style="box-shadow: 2px 2px 6px #00000022; padding: 12px;"
                        >
                            <p>{{ item.name }}</p>
                        </div>
                    </ButtonBasic>
    
                </div>
    
                <div 
                    class="gallery-images"
                >
                    <img
                        v-for="(item, index) in getPhotos"
                        class="rounded-lg shadow-sm"
                        :src="`/images/${item.name}.jpeg`"
                        :index="index"
                    >
                </div>
    
            </div>
    
        </div>
        
        <div id="baseboard-page" class="home-baseboard flex x-center">

            <div class="baseboard-frame">

                <h1 class="font-lg">Projeto por, Outpost Innovations</h1>
                <p class="font-md o-half">outpoststudioinnovations@gmail.com</p>

            </div>

        </div>

    </div>

</template>

<script>

import { photos } from "@/assets/resources/photos.js"

import * as Button from "@/components/Button"
import * as Misc from "@/components/Misc"

export default {
    data(){
        return{
            works_list: [
                {
                    icon: "box",
                    title: "Box",
                    description: `
                        Oferecemos box sob medida que unem elegância, segurança e praticidade. Trabalhamos com vidro temperado de alta resistência e acabamentos modernos, garantindo vedação eficiente, fácil limpeza e um visual sofisticado para seu banheiro.
                    `
                },
                {
                    icon: "mirror",
                    title: "Espelhos",
                    description: `
                        Espelhos personalizados que ampliam ambientes, valorizam a iluminação e trazem mais requinte ao espaço. Produzimos sob medida para banheiros, salas, academias, comércios e projetos decorativos, com instalação segura e acabamento impecável.
                    `
                },
                {
                    icon: "roof",
                    title: "Cobertura em Vidro",
                    description: `
                        Coberturas em vidro ideais para áreas externas, varandas, corredores e espaços comerciais. Utilizamos materiais resistentes e seguros que permitem a entrada de luz natural, protegem contra intempéries e agregam modernidade ao ambiente.
                    `
                },
                {
                    icon: "balcony",
                    title: "Fechamento de Sacada",
                    description: `
                        Sistemas de fechamento de sacada que proporcionam proteção contra vento, chuva e poeira, sem perder a vista e a luminosidade. Uma solução elegante que aumenta o conforto, a segurança e valoriza o imóvel.
                    `
                }                
            ],
            filtering_buttons: [
                {
                    name: "Todos",
                    filter: null,
                    selected: true,
                },
                {
                    name: "Janelas",
                    filter: "window",
                    selected: false,
                },
                {
                    name: "Portas",
                    filter: "door",
                    selected: false,
                },
                {
                    name: "Box",
                    filter: "box",
                    selected: false,
                },
                {
                    name: "Corrimão",
                    filter: "handrail",
                    selected: false,
                }
            ],
            selected_filtering: null
        }
    },
    components: {
        ...Misc,
        ...Button
    },
    methods: {
        selectFilterButtons(index){
            this.filtering_buttons = this.filtering_buttons.map((button, i) => {
                return {
                ...button,
                selected: i === index
                }
            })
        },
        openWhatsappTalk(){
            window.location.href = "https://wa.me/5511943568371"
        },
        openInstagram(){
            window.location.href = "https://www.instagram.com/do.vidros?utm_source=qr&igsh=d2t6eHZnZXo0d3Rr"
        }
    },
    computed: {
        getPhotos() {
            if (this.selected_filtering == null) {
                return photos
            }

            return photos.filter(item => item.type === this.selected_filtering)
            }
    },
    created(){
        console.log(import.meta.glob("@/"))
        
    }
}

</script>

<style lang="scss">

/* Mobile */
.home{

    scroll-behavior: smooth;

    .home-header{
        height: 100%;
        border-bottom-left-radius: var(--scale-brand-xlg);
        border-bottom-right-radius: var(--scale-brand-xlg);
        background-color: rgb(240, 240, 240);
        background-position: center;
        background-size: cover;

        .home-panel{
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 16px;
            width: 94%;

            h1{
                text-shadow: 2px 2px 8px #00000022;
                color: rgb(255, 255, 255);
                text-align: center;
            }

            p.subtitle{
                color: rgb(255, 255, 255);
                opacity: 0.6;
                text-align: center;
                width: 80%;
            }

        }

    }

    .home-about{
        .about-frame{
            display: flex;
            flex-direction: column;
            gap: var(--scale-brand-lg);
            .about-description{
                width: 100%;
            }
            .about-cards{
                display: grid;
                grid-template-rows: repeat(4, 1fr);
                gap: var(--scale-brand-lg);
            }
        }
    }

    .home-gallery{
        .gallery-images {
            column-count: 2;
            column-gap: 16px;
        }

        .gallery-images img {
            width: 100%;
            height: auto;
            margin-bottom: 16px;
            break-inside: avoid;
            display: block;
        }
    }

    .home-baseboard{
        width: 100%;
        .baseboard-frame{
            width: 100%;
            border-top-left-radius: var(--scale-brand-xlg);
            border-top-right-radius: var(--scale-brand-xlg);
            background-color: white;
            padding: 24px;
            box-shadow: 0px -2px 8px #00000011;
        }
    }

    .page-header{
        display: flex;
        flex-direction: column;
        gap: var(--scale-brand-md);
        p{
            text-align: center;
            font-size: var(--scale-brand-lg);
        }
        h1{
            font-size: 32px;
            font-weight: 100;
            text-align: center;
        }
        h2{
            font-size: 26px;
            font-weight: 100;
            text-align: center;
            margin-left: 0%;
        }
        div{
            width: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
    }

}

/* Desktop */

@media screen and (min-width: 800px) {

    .home{

        .other-pages{
            padding-left: 64px;
            padding-right: 64px;
        }

        .page-header{
            display: flex;
            flex-direction: row;
            margin-top: 64px;

            p{
                width: 140px;
                text-align: start;
                font-size: var(--scale-brand-lg);
            }
            h1{
                font-size: 32px;
                font-weight: 100;
            }
            h2{
                font-size: 32px;
                font-weight: 100;
                margin-left: 20%;
            }
            div{
                width: 100%;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
            }
        }

        .home-header{
            .home-panel{
                padding: 86px;
                align-items: flex-start;
                width: 98%;
                
                h1{
                    font-size: 46px;
                    width: 50%;
                    text-align: start;
                }
                p.subtitle{
                    text-align: start;
                }
            }
        }

        .home-about{

            .about-frame{
                display: flex;
                flex-direction: column;
                gap: var(--scale-brand-xlg);

                .about-description{
                    width: 50%;
                }

                .about-cards{
                    display: grid;
                    grid-template-columns: repeat(4, 1fr);
                    grid-template-rows: none;
                    gap: var(--scale-brand-lg);
                }

            }

        }

        .home-gallery{

            .gallery-images {
                column-count: 5;
                column-gap: 16px;
            }

            .gallery-images img {
                width: 100%;
                height: auto;
                margin-bottom: 16px;
                break-inside: avoid;
                display: block;
            }

        }

        .home-baseboard{
            width: 100%;
            .baseboard-frame{
                width: 95%;
                padding: 64px;
            }
        }
    }

}

.sub-button{
    transition: .2s;

    &:hover{
        border: 1px solid var(--color-brand-four);
    }
}

</style>
