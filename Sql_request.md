CREATE DATABASE music_store WITH OWNER = postgres;

\e music_store;

create table if not exists Genres (
	Id SERIAL primary key,
	Name VARCHAR(120) not null
	);

create table if not exists Artist (
	Id SERIAL primary key,
	Name VARCHAR(120) not null unique
	);

create table if not exists Album (
	Id SERIAL primary key,
	Name VARCHAR(120) not null,
	ReleaseAlbum integer not null
	);

create table if not exists Track (
	Id SERIAL primary key,
	Name VARCHAR(120) not null,
	Duration time not null,
	Albumid integer references Album(Id)
	);

create table if not exists ArtistGenre (
	ArtistId integer references Artist,
	GenreId integer references Genres,
	primary key (ArtistId, GenreId)
	);

create table if not exists ArtistAlbum (
	ArtistId integer references Artist,
	AlbumId integer references Album,
	primary key (ArtistId, AlbumId)
	);

create table if not exists Collection (
	Id serial primary key,
	Name VARCHAR(120) not null unique,
	ReleaseAlbum integer check (ReleaseAlbum >= 1951 and ReleaseAlbum <= 2024)
	);

create table if not exists CollectionTrack (
	CollectionId integer references Collection,
	TrackId integer references Track,
	primary key (CollectionId, TrackId)
	);