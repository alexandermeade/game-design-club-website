<script lang="ts">
    import './page.css';

    import logo from '$lib/assets/msu(1).png';
    import {Calendar, TimeGrid} from '@event-calendar/core';
    import events from "$lib/assets/events.json";
 
    let options = $state({
        view: 'timeGridWeek',
        events: events,
        slotMinTime: '15:00:00', // 3:00 PM
        slotMaxTime: '22:00:00', // 10:00 PM
        eventDidMount: (info) => {
            // Add native browser tooltip on hover
            const props = info.event.extendedProps;
            if (props && props.description) {
                info.el.title = `${info.event.title}\n\n${props.description}\n\nlocation: ${props.location}\ntime: ${props.time}`;
            }
        }
    });
</script>

<div class="page">
	<!-- Hero Section -->
	<section class="hero">
		<div class="hero-content">
			<img src={logo} alt="MSU Logo" class="hero-logo" />
			<h1>Welcome to MSU Game Design Club</h1>
			<p>A collaborative space for students to explore game design, develop projects, and connect with fellow creators</p>
			<a href="#about" class="cta-button">Learn More</a>
		</div>
	</section>

	<!-- Main Content -->
	<div class="container">
		<!-- About Section -->
		<section id="about" class="section">
			<h2 class="section-title">About Us</h2>
			<div class="about-content">
				<p>The Game Design Club at Morehead State University creates a safe, collaborative space for students from all backgrounds to discuss game design and development. Whether you're interested in programming, art, storytelling, or sound design, our club encourages both casual discussion and hands-on development.</p>
				<br>
				<p>We provide members with opportunities to create self-managed projects and walk away with tangible proof of their work—perfect for building your portfolio and gaining real-world experience.</p>
			</div>
		</section>

		<section id="goals" class="section">
			<h2 class="section-title">Our Goals</h2>
			<div class="goals-grid">
				<div class="goal-card">
					<div class="icon"></div>
					<h3>Explore All Aspects</h3>
					<p>Create a welcoming environment for exploring the edges of gaming—from storytelling and programming to art and sound design.</p>
				</div>
				<div class="goal-card">
					<div class="icon"></div>
					<h3>Collaborate & Create</h3>
					<p>Encourage members to collaborate on original projects and gain real-world experience through hands-on activities.</p>
				</div>
				<div class="goal-card">
					<div class="icon"></div>
					<h3>Build Community</h3>
					<p>Foster a supportive community where students can enjoy creating games while growing as designers, developers, and leaders.</p>
				</div>
				<div class="goal-card">
					<div class="icon"></div>
					<h3>Portfolio Building</h3>
					<p>Give members the opportunity to build real projects and present them on their resumes.</p>
				</div>
			</div>
		</section>

		<!-- Activities Section -->
		<section id="activities" class="section">
			<h2 class="section-title">Activities & Events</h2>
			<div class="activities-grid">
				<div class="activity-card">
					<div class="activity-icon"></div>
					<h3>Game Jams</h3>
					<p>Form teams and build small games around surprise prompts. Compete for prizes and celebrate your creativity in time-limited challenges.</p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
					<h3>Presentations</h3>
					<p>Student and leader-led presentations exploring topics in game design—storytelling, programming, artistic design, and more.</p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
					<h3>Debug Days</h3>
					<p>Bring your ongoing projects and receive constructive feedback and advice on design and technical aspects in a supportive setting.</p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
					<h3>Workshops</h3>
					<p>Hands-on sessions focused on specific skills—scripting, level design, art, sound integration. Learn by doing and build your portfolio.</p>
				</div>
			</div>
		</section>

		<!-- Calendar Section -->
		<section id="events" class="section">
			<h2 class="section-title">Upcoming Events</h2>
			<Calendar plugins={[TimeGrid]} {options} />
		</section>
	</div>
</div>

