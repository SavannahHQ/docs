# Understanding your Connections graph

The connections graph can produce valuable insight about the health of the online community. 

Each node is a user and each vector is a connection between 2 users. These 2 users can have at most **one** connection, which means that they have interacted, at least once, in at least one thread. 

Interaction: The participation of the 2 particular community members in the same thread. For example, they have both commented in the same Github Issue.

Savannah applies a _repulsive_ force between people and an _attractive_ force for each line of connection.

## Tight bundle

If a community has a small number of users who all participate in the same discussions, the community will be congregate in the middle, as the _attractive_ force will be larger than the _repulsive_ one. This isn't very healthy, as it means that the community is not scalable to accommodate a larger number of people, because it depends on a small number of **very active** participants. 

![Tightly bundled community](./TightBundle.png)

## Loose web

If a community is less tightly coupled, there are more people than connections, which means that the community is depending on a larger number of less involved participants. This is more sustainable, as an increase in community members will be supported by a large number of active community members who are spread out inside the community.

![A loose web of connections](./LooseWeb.png)


## Detatched circles

![Small, detatched circled](./DetatchedCircles.png)

## Central hubs

![Hubs at the center of a community](./CentralHubs.png)


## Webs of Interest

![Webs of connections concentrating on topics](./CommunityIslands.png)
