<script lang="ts">
    import Navbar from '$lib/navbar.svelte'
    import Card from '$lib/card.svelte'
    
    let contentsElems = {};

    function initializeScrollObserver() {
        document.querySelectorAll('#table-of-contentsElems a').forEach(elem => {
            contentsElems[elem.hash] = elem;
        });

        const options = {
            threshold: [0, .1, .2, .3, .4, .5, .6, .7, .8, .9, 1],
        };
        let scrollObserver = new IntersectionObserver(onIntersection, options);
        document.querySelectorAll('.section').forEach(e => scrollObserver.observe(e));
    }
    function onLoad() {
        initializeScrollObserver();
    }
    function onIntersection(entries, observer) {
        entries.forEach(e => {
            if (e.isIntersecting) {
                let link = contentsElems['#' + e.target.id];
                if (! link) {
                    console.warn(`label not found ${e.target.id}`);
                    return
                }
                if (e.intersectionRatio > 0.4) {
                    link.classList.add('selected');
                } else {
                    link.classList.remove('selected');
                }
            }
        });
    }

</script>


<style>
    .section {
        border-radius: 15px;
        overflow-y: hidden;
        background-color: lightgray;
        padding: 1rem 2rem;
        margin-bottom: 2rem;
        scroll-margin-top: 5rem;
    }
    :global(body.dark) .section {
        background-color: #0e1724;
    }
    .section h2 {
        font-size: 2.25rem;
        font-weight: bold;
        margin-bottom: 1rem;
    }
    .section:target h2 {
        text-decoration: underline;
    }
    .selected {
        font-weight: bold;
    }

    :global(body) {
        background-color: #EEEEEE;
        transition: background-color 0.3s
    }
    :global(body.dark) {
        background-color: #242529;
    }
</style>


<Navbar />

<div class="container mx-auto flex flex-col lg:flex-row">


    <!-- Table of Contents -->
    <div id="table-of-contentsElems" class="w-full lg:w-auto p-5 my-5 border rounded-xl border-gray-600 lg:fixed
        bg-white dark:bg-gray-800
        text-gray-500 dark:text-gray-300
        ">
        <h2 class="text-xl font-bold mb-4
            text-gray-700 dark:text-gray-400"
        >Contents</h2>
        <ul class="space-y-2 px-5">
            <li><a href="#publications_academic" class="hover:font-bold selected">Academic Publications</a></li>
            <li><a href="#publications_public" class="hover:font-bold">Public Philosophy</a></li>
            <li><a href="#wip" class="hover:font-bold selected">Works in Progress</a></li>

        </ul>
    </div>

    <!-- Content -->
    <div use:onLoad id="content-area" class="w-full lg:w-auto lg:ml-[15%]
        text-gray-600 dark:text-gray-300">

        <!-- PUBLICATIONS -->
        <div id="publications_academic" class="section">
            <h2> Academic Publications </h2>
            <Card
                publisher="MA Thesis"
                title="De Re Beliefs and Evidence in Legal Cases"
                link="https://philpapers.org/rec/THODRB"
                date="2021"
                text="For the past half-century, both jurisprudence and epistemology have been haunted by questions about why individual evidence (i.e., evidence which picks out a specific individual) can sufficiently justify a guilty or liable verdict while bare statistical evidence (i.e., statistical evidence which does not pick out a specific individual) does not sufficiently justify such a verdict. This thesis examines three popular justifications for such a disparity in verdicts – Judith Jarvis Thomson’s causal account, Enoch et al.’s sensitivity account, and Sarah Moss’ knowledge-first account, before critiquing each in turn. After such an analysis, the thesis then defends the claim that legal verdicts require the factfinder (e.g., the judge or jury) to have a justified de re belief (i.e., a belief about a specific object – namely the defendant), and that this doxastic requirement justifies the disparity in rulings, as it is epistemically insufficient to justify a de re belief based on bare statistical evidence alone. A brief account of how these beliefs are formed and spread is also given. After making such a distinction, the thesis then formalizes the burdens of proof of the preponderance of the evidence and beyond a reasonable doubt using the de re/de dicto distinction. Finally, the thesis pre-empts possible objections, namely by providing an account of DNA evidence as individual evidence and giving an account of how false convictions can occur on the de re view of legal proof."
            />
        </div>

        <!-- PUBLIC PUBLICATIONS -->
        <div id="publications_public" class="section">
            <h2> Public Philosophy </h2>
            Works of mine which lie outside the ivory tower.

            <Card
                publisher="Margin Notes"
                title="On the Falsity of Prevailing Ideas: The Concept of Ideology in Early Critical Theory"
                link="https://ctwgwebsite.github.io/projects/1_project/"
                date="Fall 2024"
                text="<i>Margin Notes</i> is the journal of the Critical Theory Working Group, of which I am a member. For more information, please see the CTWG tab."
                pdf="https://ctwgwebsite.github.io/assets/pdf/journal/Margin_notes_1_final_full.pdf"
                creativecommons="fa-creative-commons-by"
            />
            <Card
                publisher="Cosmonaut Mag"
                title="The Machiavellian State, Fascism, and the Tribune of the Proletariat"
                link="https://cosmonautmag.com/2022/04/the-machiavellian-state-fascism-and-the-tribune-of-the-proletariat/"
                date="29 April 2022"
                text="How Machiavelli can help us understand the bourgeois nature of fascism, and how anti-fascism must empower the proletariat"
                audio=true
            />
            <Card
                publisher="Diginativ"
                title="Spinoza with a Beard: Spinoza’s Influence on Marxism"
                link="https://diginativ.com/spinoza-with-a-beard-spinozas-influence-on-marxism/"
                date="5 May 2018 (the 200th birthday of Herr Marx)"
                text="The purpose of this essay is to analyze the effect Spinoza’s insights have had on Marxism. Thus, it will ignore similar but unrelated questions. It will not analyze the current of thinkers who came after Marx’s death who drew upon both Spinoza and Marx to form a new line of thought. This paper will not touch on the personal lives of the two men. The fact that Spinoza was a lens grinder or that Marx was a newspaper editor does not affect the argument. This paper will not touch on the points of difference between the two. The fact that two thinkers differ on a certain point does not entail that one cannot have influenced the other."
            />
        </div>
        <div id="wip" class="section">
            <h2> Works in Progress </h2>
            <Card
                title="Untitled Paper on the Ethics of Democratic Backsliding"
                text="Spoiler alert: it's bad."
            />
            <Card
                title="Untitled Paper on the Ethics of Economic Sanctions (co-authored with Michael Quick)"
                text="Spoiler alert: they're bad."
            />
            <Card
                title="Unjsut Compromises without Radical Evil (provisional title)"
                text="Spoiler alert: they're bad."
            />
        </div>
    </div>
</div>

