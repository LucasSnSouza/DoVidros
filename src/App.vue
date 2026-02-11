<template>

    <div 
        class="app h-full flex flex-column"
    >
        <div class="app-header p-lg flex y-center x-center">

            <div class="header-frame color-brand-two ghost rounded p-lg flex y-center">

                <div class="flex y-center">
                    <img 
                        style="
                            height: 30px;
                        "
                        src="/arts/dovidro-logo.png"
                    />
                </div>
                <div 
                    v-if="isMobile"
                    class="navigation-buttons flex"
                >
                    
                    <div class="p-md color-brand-one ghost rounded">
                        <MiscIcon
                            icon="menu"
                            class="bg-color-brand-one"
                            :size="[24,24]"
                        />
                    </div>

                </div>
                <div 
                    style="padding-right: var(--scale-brand-xlg);"
                    class="navigation-buttons w-full flex gap-xlg"
                    v-else
                >
                    <a href="#home-page">Inicio</a>
                    <a href="#about-page">Sobre</a>
                    <a href="#gallery-page">Galeria</a>
                </div>

            </div>

        </div>
        
        <div class="app-information h-full">
            <RouterView/>
        </div>

    </div>

</template>

<script>

import { RouterLink, RouterView } from 'vue-router'

import { useSystemStore } from '@/stores/system.js'

import { Storage } from '@/utils/storage.js'

import * as Button from "@/components/Button"
import * as Modal from "@/components/Modal"
import * as Misc from "@/components/Misc"

export default {
    data(){
        return{
        }
    },
    components: {
        ...Button,
        ...Misc,
        ...Modal
    },
    methods: {
    },
    computed: {
        isMobile(){
            return useSystemStore().getIsMobile
        }
    },
    mounted(){
    },
    created(){
        useSystemStore().isMobileVerify()
        window.addEventListener('resize', () => { useSystemStore().isMobileVerify() })
    }
}

</script>

<style lang="scss">

/* Mobile */
.app{

    .app-header{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        
        .header-frame{
            width: 100%;
            padding-left: var(--scale-brand-xlg);
            background: rgba(255, 255, 255, 0.6);
            box-shadow: 2px 2px 10px #00000022;
            backdrop-filter: blur(4px);
            z-index: 10;

            .navigation-buttons{
                width: 100%;
                justify-content: flex-end;

                a{
                    text-decoration: none;
                    color: var(--color-brand-one)
                }

            }

        }

    }

}

/* Desktop */
@media screen and (min-width: 800px) {

    .app{
        .app-header{
            .header-frame{
                width: 80%;
                .navigation-buttons{
                    justify-content: center;
                }
            }
        }
    }

}


</style>
