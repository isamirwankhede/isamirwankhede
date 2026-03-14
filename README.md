// import React from 'react'
/* eslint-disable react/prop-types */
import { Link, NavLink } from "react-router-dom";
import { TiLocationOutline } from "react-icons/ti";
import { FaSearch } from "react-icons/fa";
import { FaCaretDown } from "react-icons/fa";
import { FaShoppingCart } from "react-icons/fa";
import { IoMdClose } from "react-icons/io"; // import PropTypes from "prop-types";

import {
  SignedIn,
  SignedOut,
  SignInButton,
  SignUpButton,
  UserButton,
} from "@clerk/clerk-react";
// import { useState } from "react";

const Navbar = ({ location, getLocation, openDropdown, setOpenDropdown }) => {
  // console.log(location , getLocation);
  // console.log(location);

  // const addressHandler = () => {
  //   console.log("button clicked");
  // };

  const toggleDropdown = () => {
    setOpenDropdown(!openDropdown);
  };

  return (
    <>
      <div className="bg-[#0f1117] border-b border-white/[0.06] text-white px-6 py-0 flex gap-6 items-center h-16 sticky top-0 z-50 backdrop-blur-md shadow-[0_2px_24px_0_rgba(0,0,0,0.45)]">
        <div className="shrink-0">
          {/* logo */}
          <Link to={"/"}>
            <h1 className="text-red-500 font-extrabold text-xl tracking-tight">
              Shoppy<span className="text-white font-light">Gram</span>
            </h1>
          </Link>
        </div>

        {/* address */}
        <div className="flex gap-1 min-w-[160px] items-center cursor-pointer group select-none">
          <TiLocationOutline className="text-2xl text-red-400 shrink-0 group-hover:text-red-300 transition-colors" />
          <span className="text-xs font-medium text-gray-300 group-hover:text-white transition-colors leading-tight">
            {location ? (
              <div className="-space-y-0.5">
                <p className="text-[11px] text-gray-500 uppercase tracking-wider">Deliver to</p>
                <p className="text-white font-semibold text-sm">{location.county}</p>
                <p className="text-gray-400 text-xs">{location.state}</p>
              </div>
            ) : (
              <div>
                <p className="text-[11px] text-gray-500 uppercase tracking-wider">Deliver to</p>
                <p className="text-gray-300 font-medium text-sm">Add Address</p>
              </div>
            )}
          </span>

          <FaCaretDown
            className="text-base text-gray-400 ml-1 group-hover:text-white transition-colors"
            onClick={toggleDropdown}
          />
          {openDropdown ? (
            <div className="w-[200px] h-max shadow-[0_8px_32px_rgba(0,0,0,0.6)] z-50 bg-[#1a1d27] mt-1 fixed top-[68px] left-[172px] border border-white/10 p-5 rounded-xl">
              <h1 className="text-sm font-semibold text-white mb-4 flex justify-between items-center">
                Change Location
                <span
                  onClick={toggleDropdown}
                  className="text-gray-400 hover:text-white cursor-pointer transition-colors"
                >
                  <IoMdClose />
                </span>
              </h1>
              <button
                className="w-full bg-red-600 hover:bg-red-500 active:scale-95 text-white text-sm px-3 py-2 rounded-lg cursor-pointer transition-all duration-150 font-medium"
                onClick={getLocation}
              >
                Detect my location
              </button>
            </div>
          ) : null}
        </div>

        {/* search */}
        <div className="flex-1 max-w-[480px] flex items-center gap-0 relative">
          <input
            className="w-full px-5 py-2.5 rounded-lg bg-[#1e2130] border border-white/[0.08] text-white placeholder-gray-500 text-sm font-normal focus:outline-none focus:border-red-500/60 focus:bg-[#22263a] transition-all duration-200"
            type="text"
            name=""
            id=""
            placeholder="What are you looking for?"
          />
          <FaSearch className="absolute right-4 text-gray-500 text-sm pointer-events-none" />
        </div>

        {/* navlinks */}
        <div className="flex items-center justify-center">
          <ul className="flex gap-1 items-center justify-evenly font-medium">
            <NavLink
              to="/"
              className={({ isActive }) =>
                `px-3 py-1.5 rounded-lg text-sm transition-all duration-150 ${
                  isActive
                    ? "text-white bg-white/[0.08] border-b-2 border-red-500"
                    : "text-gray-400 hover:text-white hover:bg-white/[0.05]"
                }`
              }
            >
              <li className="list-none">Home</li>
            </NavLink>

            <NavLink
              to="/about"
              className={({ isActive }) =>
                `px-3 py-1.5 rounded-lg text-sm transition-all duration-150 ${
                  isActive
                    ? "text-white bg-white/[0.08] border-b-2 border-red-500"
                    : "text-gray-400 hover:text-white hover:bg-white/[0.05]"
                }`
              }
            >
              <li className="list-none">About</li>
            </NavLink>

            <NavLink
              to="/product"
              className={({ isActive }) =>
                `px-3 py-1.5 rounded-lg text-sm transition-all duration-150 ${
                  isActive
                    ? "text-white bg-white/[0.08] border-b-2 border-red-500"
                    : "text-gray-400 hover:text-white hover:bg-white/[0.05]"
                }`
              }
            >
              <li className="list-none">Product</li>
            </NavLink>

            <NavLink
              to="/contact"
              className={({ isActive }) =>
                `px-3 py-1.5 rounded-lg text-sm transition-all duration-150 ${
                  isActive
                    ? "text-white bg-white/[0.08] border-b-2 border-red-500"
                    : "text-gray-400 hover:text-white hover:bg-white/[0.05]"
                }`
              }
            >
              <li className="list-none">Contact</li>
            </NavLink>
          </ul>
        </div>

        {/* cart */}
        <Link to={"/cart"} className="relative p-2 rounded-lg hover:bg-white/[0.06] transition-colors shrink-0">
          <FaShoppingCart className="h-5 w-5 text-gray-300 hover:text-white transition-colors" />
          <span className="bg-red-600 text-white text-[10px] font-bold px-1.5 py-0.5 rounded-full absolute -top-1 -right-1 min-w-[18px] text-center leading-tight">
            {0}
          </span>
        </Link>

        {/* signup */}
        <div className="flex gap-2 items-center shrink-0">
          <div className="flex gap-2">
            <SignedOut>
              <SignInButton className="bg-transparent border border-white/20 hover:border-white/40 text-gray-300 hover:text-white text-sm px-4 py-2 rounded-lg transition-all duration-150 cursor-pointer" />
              <SignUpButton className="bg-red-600 hover:bg-red-500 text-white text-sm px-4 py-2 rounded-lg transition-all duration-150 cursor-pointer font-medium" />
            </SignedOut>
          </div>

          <div className="flex">
            <SignedIn>
              <UserButton className="w-[32px] h-[32px]" />
            </SignedIn>
          </div>
        </div>
      </div>
    </>
  );
};

// Navbar.propTypes = {
//   location: PropTypes.shape({
//     county: PropTypes.string,
//     state: PropTypes.string,
//     city: PropTypes.string,
//   }),
//   getLocation: PropTypes.func,
// };

export default Navbar;
