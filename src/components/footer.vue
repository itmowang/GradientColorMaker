<template>
    <div class="footer">
        <div class="footer-content">
            <div>
                <h2>Tools</h2>
                <ul>
                    <li v-for="item in state.tools"> {{ item.name }} </li>
                </ul>
            </div>
            <div>
                <h2>More</h2>
                <ul>
                <li v-for="item in state.more"> {{ item.name }} </li>
            </ul>
            </div>
            <div>
                <h2>Jobs</h2>
                <ul>
                <li v-for="item in state.jobs"> {{ item.name }} </li>
                </ul>
                <h2>Apps</h2>
                <ul>
                <li v-for="item in state.apps"> {{ item.name }} </li>
            </ul>
            </div>
            <div>
                <h2>Company</h2>
                <ul>
                <li v-for="item in state.company"> {{ item.name }} </li>
            </ul>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref, reactive } from 'vue'

const state = reactive({
    tools: [
        {
            name: 'Generate your palettes',
            link: ''
        },
        {
            name: 'Explore popular palettes',
            link: ''
        },
        {
            name: 'Extract palette from image',
            link: ''
        },
        {
            name: 'Contrast checker',
            link: ''
        },
        {
            name: 'Change image colors',
            link: ''
        },
        {
            name: 'Color picker',
            link: ''
        },
        {
            name: 'Browse free fonts',
            link: ''
        },
    ],
    more: [
        {
            name: "List of colors",
            link: ""
        },
        {
            name: "Browse gradients",
            link: ""
        },
        {
            name: "Create a gradient",
            link: ""
        },
        {
            name: "Make a gradient palette",
            link: ""
        },
        {
            name: "Image converter",
            link: ""
        },
        {
            name: "Create a collage",
            link: ""
        },
        {
            name: "Font Generator",
            link: ""
        },
    ],
    jobs: [
        {
            name: "Find your next job",
            link: ""
        },
        {
            name: "Post a job",
            link: ""
        }
    ],
    company: [
        {
            name: "About",
            link: ""
        },
        {
            name: "Contact",
            link: ""
        },
        {
            name: "Privacy Policy",
            link: ""
        },
        {
            name: "Terms of Service",
            link: ""
        },
        {
            name: "Cookie Policy",
            link: ""
        },
        {
            name: "Press Kit",
            link: ""
        },
        {
            name: "Colors API",
            link: ""
        },
    ],
    apps: [
        {
            name: "iOS APP",
            link: ""
        },
        {
            name: "Android APP",
            link: ""
        },
        {
            name: "Figma Plugin",
            link: ""
        },
        {
            name: "Adobe Extension",
            link: ""
        },
        {
            name: "Chrome Extension",
            link: ""
        },
        {
            name: "Instagram Page",
            link: ""
        },
    ]
})
</script>
<style lang="less">
.footer {
    border-top: 1px solid #e6e6e6;
    background-color: #f7f7f8;
    height: 100%;

    .footer-content {
        width: 1200px;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
        padding: 20px 0;

        ul {
            list-style: none;
            padding: 0;
            li {
                font-size: 14px;
                color: black;
                cursor: pointer;
                font-weight: 400;
                margin: 10px 0;
            }
            li:hover{
                color: #0066ff;
            }
        }

        h2 {
            font-size: 24px;
            color: #333;
            cursor: pointer;
            font-weight: 600;
        }



    }
}</style>