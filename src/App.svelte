<script>
  import { onMount } from "svelte";
  import axios from "axios";

  // export let name;
  let tattoo_machine = "/img/tattoo_machine.png";
  const instagramRegExp = new RegExp(
    /<script type="text\/javascript">window\._sharedData = (.*)<\/script>/
  );

  const fetchInstagramPhotos = async (accountUrl) => {
		console.log(accountUrl)
    console.log(axios);
    const response = await axios.get(accountUrl);
    const json = JSON.parse(response.data.match(instagramRegExp)[1]);
    const edges =
      json.entry_data.ProfilePage[0].graphql.user.edge_owner_to_timeline_media.edges.splice(
        0,
        8
      );
    const photos = edges.map(({ node }) => {
      return {
        url: `https://www.instagram.com/p/${node.shortcode}/`,
        thumbnailUrl: node.thumbnail_src,
        displayUrl: node.display_url,
        caption: node.edge_media_to_caption.edges[0].node.text,
      };
    });
    return photos;
  };

	const getRandomInstagramPic = () => {
		fetch("https://api.allorigins.win/get?url=https://www.instagram.com/marcopulesh/")
		.then(response => {
			if (response.ok) {
				return response.json()
				// return response.json()
			}
			console.log(response)
		})
		.then(data => {
			let contents = data.contents
			var doc = new DOMParser().parseFromString(data.contents, "text/html");
			console.log(doc.querySelector('body'))
		})
	}

  onMount(() => {
    // fetchInstagramPhotos("https://www.instagram.com/marcopulesh/");
		getRandomInstagramPic()
  });
</script>

<main>
  <div class="container">
    <h1>Marco Di Sotto</h1>
    <p>Tattoo Artist</p>
    <img class="tattoo_machine" src={tattoo_machine} alt="A tattoo machine." />
  </div>
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: 100vh;
  }

  .container {
    position: relative;
  }

  .tattoo_machine {
    position: absolute;
    top: -210px;
    left: -50px;
    width: 100%;
    height: auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 2em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }

    h1 {
      font-size: 4em;
    }

    .tattoo_machine {
      top: -357px;
      left: -180px;
      width: 90%;
    }
  }
</style>
