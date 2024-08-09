<template>
  <header class="py-12 px-4 sm:px-6 lg:px-8">
    <div class="relative mx-auto max-w-[37.5rem] pt-20 text-center pb-20">
      <badge :label="`Developer-First Platform as a Service`" class="absolute -top-6 right-0 md:static mb-4" />
      <div class="flex items-center justify-center space-x-3">
        <h1 class="text-4xl font-extrabold tracking-tight text-slate-700 sm:text-5xl">
          Deploy your Nuxt App
          <span class="block">with Zerops</span>
        </h1>
      </div>
      <p class="mt-4 text-base leading-7 text-slate-600">
        Nuxt SSR Node.js example running on Zerops.
        Deploy and test yourself with a single click.
      </p>
      <a href="https://app.zerops.io/recipe/nextjs-nodejs" target="_blank"
        className="text-lg inline-block hover:no-underline text-white">
        <span
          className="deploybutton rounded-full flex flex-row items-center justify-center space-x-4 hover:-translate-y-1 duration-300 text-white">
          <span>Deploy on Zerops</span>
          <svg xmlns="http://www.w3.org/2000/svg" enableBackground="new 0 0 24 24" height="22px" viewBox="0 0 24 24"
            width="24px" fill="#fff">
            <g>
              <rect fill="none" height="24" width="24"></rect>
            </g>
            <g>
              <g>
                <path
                  d="M6,15c-0.83,0-1.58,0.34-2.12,0.88C2.7,17.06,2,22,2,22s4.94-0.7,6.12-1.88C8.66,19.58,9,18.83,9,18C9,16.34,7.66,15,6,15 z M6.71,18.71c-0.28,0.28-2.17,0.76-2.17,0.76s0.47-1.88,0.76-2.17C5.47,17.11,5.72,17,6,17c0.55,0,1,0.45,1,1 C7,18.28,6.89,18.53,6.71,18.71z M17.42,13.65L17.42,13.65c6.36-6.36,4.24-11.31,4.24-11.31s-4.95-2.12-11.31,4.24l-2.49-0.5 C7.21,5.95,6.53,6.16,6.05,6.63L2,10.69l5,2.14L11.17,17l2.14,5l4.05-4.05c0.47-0.47,0.68-1.15,0.55-1.81L17.42,13.65z M7.41,10.83L5.5,10.01l1.97-1.97l1.44,0.29C8.34,9.16,7.83,10.03,7.41,10.83z M13.99,18.5l-0.82-1.91 c0.8-0.42,1.67-0.93,2.49-1.5l0.29,1.44L13.99,18.5z M16,12.24c-1.32,1.32-3.38,2.4-4.04,2.73l-2.93-2.93 c0.32-0.65,1.4-2.71,2.73-4.04c4.68-4.68,8.23-3.99,8.23-3.99S20.68,7.56,16,12.24z M15,11c1.1,0,2-0.9,2-2s-0.9-2-2-2s-2,0.9-2,2 S13.9,11,15,11z">
                </path>
              </g>
            </g>
          </svg>
        </span>
      </a>
      <p>Deploying will import the following structure (zerops-project-import.yml)
        and use following (zerops.yml) instructions to build and deploy your app:</p>
      <div class="flex flex-row gap-10 justify-center">
        <div class="flex flex-col gap-5">
          <Codeblock :code="importyaml" />
          <div className="flex flex-col py-10 h-[260px] rounded-md gap-5 px-10 border-[#E6E6E6] border">
            <a href="https://github.com/zeropsio/recipe-nuxt-nodejs" target="_blank"
              className="primarybutton rounded-full text-center text-md duration-300 hover:no-underline">Recipe Source
              Code</a>
            <a href="https://discord.com/invite/WDvCZ54" target="_blank"
              className="discordbutton rounded-full text-center text-md duration-300 hover:no-underline">Discord
              Server</a>
            <a href="https://docs.zerops.io" target="_blank"
              className="zeropsbutton rounded-full text-center text-md duration-300 hover:no-underline">Zerops
              Documentation</a>
          </div>

        </div>
        <Codeblock :code="zeropsyml" />
      </div>
    </div>
  </header>
</template>

<script setup>
import Codeblock from "./Codeblock.vue"
const importyaml = `project:
  name: recipe-nuxt
  tags:
    - zerops-recipe

services:
  - hostname: app
    type: nodejs@20e
    buildFromGit: https://github.com/zeropsio/recipe-nuxt-nodejs
    enableSubdomainAccess: true`.trimStart();

const zeropsyml = `zerops:
  - setup: app
    build:
      base: nodejs@20
      buildCommands:
        - pnpm i
        - pnpm build
      deployFiles:
        - .output
        - public
        - node_modules
        - package.json
    run:
      base: nodejs@20
      ports:
        - port: 3000
          httpSupport: true
      start: pnpm start
      `.trimStart();
</script>

<style scoped>
.deploybutton {
  background-color: #00b1a3;
  padding-left: 6rem;
  padding-right: 6rem;
  padding-top: 0.62rem;
  padding-bottom: 0.62rem;
  font-weight: 700;
  color: #fff;
  transition: 300ms;
}

.deploybutton:hover {
  background-color: #3cbdb2;
}

.primarybutton {
  background-color: #131313;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  font-weight: 600;
  color: #fff;
  transition: 300ms;
}

.primarybutton:hover {
  background-color: #4a4a4a;
}

.discordbutton {
  border: #d4d4d4 solid 1px;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  font-weight: 600;
  color: #131313;
  transition: 300ms;
}

.discordbutton:hover {
  background-color: #F9F9F9;
}

.zeropsbutton {
  border: #d4d4d4 solid 1px;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  font-weight: 600;
  color: #131313;
  transition: 300ms;
}

.zeropsbutton:hover {
  background-color: #F9F9F9;
}
.form-input {
  @apply block h-10 w-full rounded-md bg-white pr-3 pl-12 text-slate-900 shadow-md shadow-black/5 ring-1 ring-slate-900/5 placeholder:text-slate-400 focus:outline-none focus:ring-2 focus:ring-primary sm:text-sm sm:leading-6;
}
.form-submit {
  @apply inline-flex justify-center rounded-lg text-sm font-semibold py-2.5 px-4 bg-slate-900 text-white hover:bg-slate-700 ml-4 flex-none;
}
</style>
